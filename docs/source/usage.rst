Usage
=====

.. _installation:

Installation
------------

Dependencies
------------------
Rdeval relies on two libraries that should be correctly installed in your system:
- Openssl, to compute md5sums
- htslib, to work with BAM and CRAM files

To use rdeval, you can either:
- download precompiled builds for your platform from the latest release `here <https://github.com/vgl-hub/rdeval/releases>`_
- compile it from source

Source compilation
------------------

.. code-block:: console

   (.venv) $ pip install lumache

Creating recipes
----------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

