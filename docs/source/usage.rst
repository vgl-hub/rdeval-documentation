Usage
#####

.. _installation:

Installation
************

Dependencies
============
Rdeval relies on two libraries that should be correctly installed in your system:

* `Openssl <https://www.openssl.org/>`_, to compute md5sums
* `Htslib <https://github.com/samtools/htslib>`_, to work with BAM and CRAM files

To use rdeval, you can either:

* download precompiled builds for your platform from the latest release `here <https://github.com/vgl-hub/rdeval/releases>`_
* `compile it from source<Compilation from source>`_

Compilation from source
=======================

To compile rdeval you need the libraries listed in the `dependency section<Dependencies>`_ correctly installed under your path, and then simply run the following command in rdeval's main folder:

.. code-block:: console

   make -j

Useful commands
***************