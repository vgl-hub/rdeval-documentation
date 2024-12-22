Usage
#####

Installation
************

Dependencies
============
Rdeval relies on two libraries that should be correctly installed in your system:

* `Openssl <https://www.openssl.org/>`_, to compute md5sums
* `Htslib <https://github.com/samtools/htslib>`_, to work with BAM and CRAM files

To use rdeval, you can either:

* download precompiled builds for your platform from the latest release `here <https://github.com/vgl-hub/rdeval/releases>`_
* :ref:`compile it from source <Compilation from source>`

Compilation from source
=======================

To compile rdeval you need the libraries listed in the :ref:`dependency section <Dependencies>` correctly installed under your path, and then simply run the following command in rdeval's main folder:

.. code-block:: console

   make -j

Useful commands
***************