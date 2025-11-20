PacBio CiFi reads
*****************

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