Memory usage and parallel processing
####################################

Overview

---

The latest versions of `rdeval` are designed to be very memory efficient.
Internally, `rdeval` uses an MPMC (multi-producer / multi-consumer) queue
implemented as a bounded ring buffer. This design provides strict, predictable
memory bounds while still running at (or very close to) theoretical full
throughput on modern CPUs.

Default parallelism

---

By default (values can be changed in the CLI), `rdeval` uses:

* `parallel_files = 4`
* `decompression_threads = 4`
* `compression_threads = 6`

This means:

* Up to 4 input files are processed in parallel. If you provide more than 4
  input files, `rdeval` processes them in batches of 4 (first 4, then the
  next 4, and so on).
* For BAM/CRAM input, each file can use up to 4 decompression threads.
* These are **threads**, not physical cores, so it is usually fine to have more
  threads than hardware cores; the scheduler will multiplex them.

Input-side ring buffer

---

The main input pipeline uses a bounded ring buffer shared between producer and
consumer threads.

* Let:

  * `producersN` be the number of producer threads (i.e. input file readers)
  * `consumersN` be the number of consumer threads (typically the total
    worker threads in the pipeline)

* The number of buffers in the ring is:

  .. code-block:: text

  buffersN = (consumersN + producersN) * 2

* Each individual buffer is by default ~1,000,000 bp, i.e. ~1 MB of sequence
  data.

Since `consumersN` corresponds to the total number of active threads in the
pipeline, the total memory allocated for this ring buffer is roughly:

.. code-block:: text

total_input_buffer_memory  ≈  buffersN × 1 MB

# Example: single compressed FASTQ file

If your machine has, for instance, 32 threads and you allow `rdeval` to use
all of them for a single input file, the upper bound for the input-side
buffering is approximately:

.. code-block:: text

consumersN  ≈ 32
producersN  ≈ 1
buffersN    = (32 + 1) * 2  ≈ 66

total_input_buffer_memory  ≈ 66 MB

In internal benchmarks, the actual memory footprint is minimal in practice,
and substantially smaller than the <4 GB previously reported in the original
manuscript for older configurations. If you observe a significantly larger
memory usage under typical workloads, please let us know so we can investigate.

Output-side ring buffer (writing to disk)

---

When the user requests writing data to disk (e.g. converting FASTQ>BAM), `rdeval` uses a **second** bounded ring buffer for the
output stage. This is governed by:

.. code-block:: text

outBuffersN = consumersN * 4 + 1

where `consumersN` is again the total number of worker threads in the
pipeline. Each output buffer is of comparable size (on the order of ~1 MB),
so the additional memory required for the output ring is approximately:

.. code-block:: text

total_output_buffer_memory  ≈  outBuffersN × 1 MB

Thus, when writing to disk, a good upper bound for total buffer memory is:

.. code-block:: text

total_buffer_memory  ≈  (buffersN + outBuffersN) × 1 MB

In most practical use cases this remains modest compared to available RAM
on typical analysis nodes.

Practical recommendations on clusters

---

Even though `rdeval` can in principle process many files on a single node
with a large number of CPUs without significant performance degradation, in
cluster environments it is often more convenient and robust to:

1. Generate **individual `.rd` files** for each input file (or logical
   group of inputs).
2. Combine the resulting `.rd` files at the end of the pipeline.

The final combination step is extremely fast and is described in detail in
the usage documentation:

* `rdeval usage: generating and processing .rd files <https://rdeval-documentation.readthedocs.io/en/latest/usage.html#to-output-data-to-a-rd-file-then-to-run-rdeval-on-the-rd-file>`_

This approach simplifies resource management (especially memory and I/O) on
multi-user clusters while preserving parallelism and throughput. It also enables the visualization of multiple .rd results in a single report <https://rdeval-documentation.readthedocs.io/en/latest/rd.html#to-generate-a-html-or-pdf-file>

Notes and feedback

---

The current configuration (defaults, buffer sizes and thread scheduling) has
been tuned for typical high-throughput use cases, but has not yet been
exhaustively benchmarked across all possible hardware and input types.

Different combinations of:

* `parallel_files`
* `decompression_threads`
* `compression_threads`
* `max-memory`

may yield better performance or memory usage on specific systems, especially
for highly compressed BAM/CRAM inputs where I/O and decompression behave
differently from FASTQ.

We welcome feedback and real-world benchmarks from users to further refine
these defaults and improve both performance and memory efficiency.
