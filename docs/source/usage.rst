Usage
#####

Installation
************

Dependencies
============
Rdeval relies on three libraries that should be correctly installed in your system:

* `Openssl <https://www.openssl.org/>`_, to compute md5sums
* `Htslib <https://github.com/samtools/htslib>`_, to work with BAM and CRAM files
* `zlib <https://github.com/madler/zlib>`_, required for the gzip compression and decompression

To use rdeval, you can either:

* download precompiled builds for your platform from the latest release `here <https://github.com/vgl-hub/rdeval/releases>`_
* :ref:`compile it from source <Compilation from source>`

Compilation from source
=======================

To compile rdeval you need the libraries listed in the :ref:`dependency section <Dependencies>` correctly installed under your path, and then simply run the following command in rdeval's main folder:

.. code-block:: console

   make -j

Troubleshooting the Installation
================================

If you run into issues when compiling rdeval, ensure you have the above dependencies installed.
Once you have confirmed they are installed, run the make clean command below, before rerunning the make -j command in rdevals main folder:

.. code-block:: console

   make clean
   make -j

Useful commands
***************

Help and Usage:
===============
To see a list of the usage of rdeval:

.. code-block:: console

   rdeval --help

Output size list, based on unsorted ('u'), sorted ('s'), histogram ('h') or inverse cumulative table ('c') [-s/--out-size]:
=================
.. code-block:: console

   redval -s u /path/to/testfiles/random1.fastq
   redval -s s /path/to/testfiles/random1.fastq
   redval -s h /path/to/testfiles/random1.fastq
   redval -s c /path/to/testfiles/random1.fastq

To generate a read summary:
===========================
.. code-block:: console

   rdeval -r /path/to/testFiles/random1.fasta

To generate stats:
==================
.. code-block:: console

   rdeval /path/to/data > /path/to/outfile.stats

To obtain a distribution of quality for each read (c) or both length and quality(l):
====================================================================================
.. code-block:: console

   rdeval /path/to/testfiles/random1.fastq -q c
   rdeval /path/to/testfiles/random1.fastq -q l

To generate a per-read report:
==============================
.. code-block:: console

   rdeval --sequence-report /path/to/testFiles/random1.fasta

To filter the reads to be assessed, by length ('l') or quality ('q'), or both:
==============================================================================
.. code-block:: console

   rdeval -f 'l>10' /path/to/testFiles/random1.fasta
   rdeval -f 'q>10' /path/to/testFiles/random1.fasta
   rdeval -f 'l>10 & q>10' /path/to/testFiles/random1.fasta

To exclude data from analysis, based on read header information in a list [-e/--exclude-list]:
==========================================================================
.. code-block:: console

   rdeval -e header.txt /path/to/testFiles/random1.fasta

To include data in the analysis, based on read header information in a list [-i/include-list]:
==========================================================================
.. code-block:: console

   rdeval -i header.txt /path/to/testFiles/random1.fasta

To write reads to a file or generate an rd summary file (output options: fa*[.gz], bam, cram, rd):
========================================================
.. code-block:: console

   rdeval -o output1.fa /path/to/testFiles/random1.fastq

To compress all the homopolymers longer than 'n' in the input:
==============================================================
.. code-block:: console

   rdeval --homopolymer-compress 1 /path/to/testFiles/random1.fastq

To subsample reads (requires an float between 0 and 1):
===================
.. code-block:: console
    rdeval --sample 0.5 /path/to/testFiles/random1.fastq

To make subsampling reproducible, use the '--random-seed <int>' option:
===================
.. code-block:: console
    rdeval --sample 0.5 --random-seed 1 /path/to/testFiles/random1.fastq

To print md5 of a .rd file:
===========================
.. code-block:: console
   rdeval --md5 /path/to/testFiles/random2.rd

To generate a HTML file:
========================
This requires the following packages also be installed: tidyverse (v2.0.0), ggExtra (v0.10.1), bit64 (v4.5.2)
.. code-block:: console

   R -e "rmarkdown::render('${RDEVAL}/figures.Rmd', output_file='[output].html')" --args "[rd-file-1].rd" "[rd-file-2].rd"

To display the software version number [-v/--version]:
=======================================
.. code-block:: console
   rdeval -v 

Other command options are available by using the :ref:`help <Help and Usage>` function, described above.
