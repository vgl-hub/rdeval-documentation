Usage
#####

Installation
************

Dependencies
============
Rdeval relies on three libraries that should be correctly installed in your system:

* `Openssl <https://www.openssl.org/>`_, to compute md5sums
* `Htslib <https://github.com/samtools/htslib>`_, to work with BAM and CRAM files
* `zlib <https://github.com/madler/zlib>`

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
---------------
To see a list of the useage of rdeval:
.. _help-reference-label:
.. code-block:: console
   rdeval --help

Output size list:
-----------------
.. code-block:: console
   redval -s

To generate stats:
------------------
.. code-block:: console
   rdeval /path/to/data > /path/to/outfile.stats

To obtain a distribution of quality length:
-------------------------------------------
.. code-block:: console
   rdeval testfiles/random1.fastq -ql

Other command options are available by using the :ref:`help-reference-lable <-help>` function, above.