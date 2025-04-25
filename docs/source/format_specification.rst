Rdeval snapshot format specification
#####

Introduction
************
Rdeval can optionally generate read 'snapshots', i.e. highly condensed representation of relevant read features that can then be stored in rdeval's own highly compressed .rd files, which are described hereafter.

.rd file format specification
*****************************
An .rd file is currently made of a binary header followed by a gzip-compressed binary data section.

Header
======
The header contains information the files that went into the generation of the snapshot file along with their md5sum values. The first 4 bytes correspond to a uint32 with the # files, followed by the following structure for each file:

.. csv-table:: Header specification
   :file: header.csv
   :header-rows: 1

Data
======
The header is followed by a binary uint64 with the size of the uncompressed data. Data follows as gzip-compressed binary data structured as:

.. csv-table:: Data specification
   :file: data.csv
   :header-rows: 1

len8, len16, len64 help compression under different scenarios of read length distribution, and refer to specialized data structures to store each individual read length/quality pair. These are contiguous pairs for each read of uint8/uint16/uint64 (read length) and float (read quality). Reads are pre-sorted descending by size and then by quality

Examples of how to read .rd files are provided for C/C++ and R `here <https://github.com/vgl-hub/rdeval/blob/main/src/reads.cpp>`_ and `here <https://github.com/vgl-hub/rdeval/blob/main/rdeval_interface.R>`_.