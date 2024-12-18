Usage
#####

.. _installation:

Installation
************

Dependencies
============
Rdeval relies on two libraries that should be correctly installed in your system:

* Openssl, to compute md5sums
* htslib, to work with BAM and CRAM files

To use rdeval, you can either:

* download precompiled builds for your platform from the latest release `here <https://github.com/vgl-hub/rdeval/releases>`_
* compile it from source

Compilation from source
=======================

To compile rdeval you need the libraries listed in the dependency section correctly installed under your path, and then simply run the following command in rdeval's main folder:

.. code-block:: console

   make -j

Useful commands
***************