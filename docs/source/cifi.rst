PacBio CiFi reads
*****************

rdeval supports **PacBio CiFi** data, allowing:

* in-silico restriction digestion of reads   
* output of all fragment combinations  
* compatibility with FASTA/FASTQ/BAM/CRAM I/O  

Two options enable these features:

``--cifi-enzyme <string>``
--------------------------

Specifies the restriction enzyme motif used for in-silico digestion.

Example:

.. code-block:: console

   rdeval --cifi-enzyme DpnII testFiles/cifi_reads.fastq -o cifi_reads.digested.fastq


``--cifi-out-combinations``
---------------------------

Outputs **all possible combinations** of digested fragments per read as paired-end (PE) reads.

Example:

.. code-block:: console

   rdeval --cifi-enzyme DpnII --cifi-out-combinations testFiles/cifi_reads.fastq -p rdeval_

For each input file, this will generate two PE files following the naming pattern:

- ``<prefix>_1.<ext>``
- ``<prefix>_2.<ext>``


Reference
---------

CiFi: Accurate long-read chromosome conformation capture with low-input requirements  
https://www.biorxiv.org/content/10.1101/2025.01.31.635566v2
