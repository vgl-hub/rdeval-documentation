Usage
#####

Installation
************

To install with conda (preferred method)
========================================

To install rdeval with conda, first you should install conda (https://github.com/conda-forge/miniforge, please view the README.md on this page for further details), then rdeval using the following commands:

.. code-block:: console

   curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
   bash Miniforge3-Linux-x86_64.sh

Once conda is installed, rdeval can then be installed using the following command:

.. code-block:: console

   conda create --name rdeval --channel conda-forge --channel bioconda --override-channels --strict-channel-priority rdeval

Before using rdeval, you will need to activate the conda environment created, using the following command:

.. code-block:: console

   conda activate rdeval


Standard installation
======================

Dependencies
------------
Rdeval relies on three libraries that should be correctly installed in your system:

* `Openssl <https://www.openssl.org/>`_, to compute md5sums
* `Htslib <https://github.com/samtools/htslib>`_, to work with BAM and CRAM files
* `zlib <https://github.com/madler/zlib>`_, required for the gzip compression and decompression

To use rdeval, you can either:

* download precompiled builds for your platform from the latest release `here <https://github.com/vgl-hub/rdeval/releases>`_
* :ref:`compile it from source <Compilation from source>`


Compilation from source
-----------------------

To compile rdeval you need the libraries listed in the :ref:`dependency section <Dependencies>` correctly installed under your path, and then simply run the following command in rdeval's main folder:

.. code-block:: console

   make -j


To use rdeval with the static linked binary (linux distribution only)
======================================================================

In cases where installation with conda or installing dependencies proves difficult, a fully static binary file is availble as a .zip file on the Releases page for rdeval, starting from v0.0.6 (https://github.com/vgl-hub/rdeval/releases). To use this binary file:

Download the binary .zip file to your linux machine.
Unzip the .zip file:

.. code-block:: console

   unzip rdeval.v0.0.6-linux-static.zip

Make the unzipped binary file executable:

.. code-block:: console

   chmod +x rdeval_static_binary

Run the executable binary file:

.. code-block:: console

   ./rdeval_static_binary rdeval/testFiles/random1.fasta


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

   rdeval -s u rdeval/testFiles/random1.fastq
   rdeval -s s rdeval/testFiles/random1.fastq
   rdeval -s h rdeval/testFiles/random1.fastq
   rdeval -s c rdeval/testFiles/random1.fastq

To generate a read summary:
===========================
.. code-block:: console

   rdeval -r rdeval/testFiles/random1.fasta

To generate stats:
==================
.. code-block:: console

   rdeval /path/to/data > /path/to/outfile.stats

To obtain a distribution of quality for each read (q) or both length and quality(a):
====================================================================================
.. code-block:: console

   rdeval rdeval/testFiles/random1.fastq -qq
   rdeval rdevaltestFiles/random1.fastq -qa

To generate a per-read report:
==============================
.. code-block:: console

   rdeval --sequence-report rdeval/testFiles/random1.fasta

To filter the reads to be assessed, by length ('l') or quality ('q'), or both:
==============================================================================
.. code-block:: console

   rdeval -f 'l>10' rdeval/testFiles/random1.fasta
   rdeval -f 'q>10' rdeval/testFiles/random1.fasta
   rdeval -f 'l>10 & q>10' rdeval/testFiles/random1.fasta

To exclude data from analysis, based on read header information in a list [-e/--exclude-list]:
==========================================================================
.. code-block:: console

   rdeval -e header.txt rdeval/testFiles/random1.fasta

To include data in the analysis, based on read header information in a list [-i/include-list]:
==========================================================================
.. code-block:: console

   rdeval -i header.txt rdeval/testFiles/random1.fasta

To write reads to a file or generate an rd summary file (output options: fa*[.gz], bam, cram, rd):
========================================================
.. code-block:: console

   rdeval -o output1.fa rdeval/testFiles/random1.fastq

To compress all the homopolymers longer than 'n' in the input:
==============================================================
.. code-block:: console

   rdeval --homopolymer-compress 1 rdeval/testFiles/random1.fastq

To subsample reads (requires an float between 0 and 1):
===================
.. code-block:: console

    rdeval --sample 0.5 rdeval/testFiles/random1.fastq

To make subsampling reproducible, use the '--random-seed <int>' option:
===================
.. code-block:: console

    rdeval --sample 0.5 --random-seed 1 rdeval/testFiles/random1.fastq

To print md5 of a .rd file:
===========================
.. code-block:: console

   rdeval --md5 rdeval/testFiles/random2.rd

To output data to a .rd file, then to run rdeval on the .rd file:
=============================
.. code-block:: console

   rdeval -output1.rd rdeval/testFiles/random1.fastq
   rdeval output1.rd 
   rdeval output1.rd -qa

To read a .bam or .cram file:
=============================
.. code-block:: console

   rdeval rdeval/testFiles/random3.bam
   rdeval rdeval/testFiles/random3.cram

To display the software version number [-v/--version]:
=======================================
.. code-block:: console

   rdeval -v 

Other command options are available by using the :ref:`help <Help and Usage>` function, described above.

Generation of .rd reports
#########################

To generate a HTML or PDF file:
===============================
Generating plots requires the following packages in R:

* `bit64 <https://cran.r-project.org/web/packages/bit64/index.html>`_, (v4.5.2+)
* `tidyverse <https://www.tidyverse.org/>`_, (v2.0.0+)
* `ggExtra <https://cran.r-project.org/web/packages/ggExtra/vignettes/ggExtra.html>`_, (v0.10.1+)
* `plotly <https://plotly.com/r/>`_, (v4.10.4+)

The packages can be installed in an R console with the following instructions:

.. code-block:: console

   install.packages("bit64", "tidyverse", "ggExtra", "plotly")

Generating a PDF file requires installing a LaTeX distribution such as TinyTeX. TinyTeX can be installed using the following commands:

.. code-block:: console

   install.packages("tinytex")
   tinytex::install_tinytex()

Please note that only static plots can be rendered in PDF format. **generate_report.sh** will auomatically generate a HTML file if given "-f pdf" and "--interactive" as arguments.

The usage is as follows:

.. code-block:: console

   generate_report.sh -i input1.rd [input2.rd ...] -o output_file [--interactive] [-h]

   Arguments:
   -i, --input     Input rd file(s)
   -o, --output    Output filename (must end in .html or .pdf)
   --interactive   Enable interactive plotting, only supported in html (default: static)
   -h, --help      Show help


PacBio CiFi read digestion
##########################

rdeval supports **PacBio CiFi** data, allowing:

* in-silico restriction digestion of reads   
* output of all fragment combinations  
* compatibility with FASTA/FASTQ/BAM/CRAM input  

Two options enable these features:

### ``--cifi-enzyme <string>``
Specifies the restriction enzyme motif used for in-silico digestion.

Example:

.. code-block:: console

   rdeval --cifi-enzyme DpnII cifi_reads.fastq -o cifi_reads.digested.fastq


### ``--cifi-out-combinations``
Outputs **all possible combinations** of digested fragments per read as PE (paired-end) reads.

Example:

.. code-block:: console

   rdeval --cifi-enzyme DpnII --cifi-out-combinations cifi_reads.fastq -p rdeval_
   
For each input file, this will generate two PE files with the same file extension, the user prefix (``-p``), and ``_1``, ``_2`` suffixes to the file names.

### Reference

CiFi: Accurate long-read chromosome conformation capture with low-input requirements
https://www.biorxiv.org/content/10.1101/2025.01.31.635566v2
