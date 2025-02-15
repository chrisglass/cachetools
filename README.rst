cachetools
========================================================================

.. image:: https://img.shields.io/pypi/v/cachetools
   :target: https://pypi.org/project/cachetools/
   :alt: Latest PyPI version

.. image:: https://img.shields.io/readthedocs/cachetools
   :target: https://cachetools.readthedocs.io/
   :alt: Documentation build status

.. image:: https://img.shields.io/github/workflow/status/tkem/cachetools/CI
   :target: https://github.com/tkem/cachetools/actions/workflows/ci.yml
   :alt: CI build status

.. image:: https://img.shields.io/codecov/c/github/tkem/cachetools/master.svg
   :target: https://codecov.io/gh/tkem/cachetools
   :alt: Test coverage

.. image:: https://img.shields.io/github/license/tkem/cachetools
   :target: https://raw.github.com/tkem/cachetools/master/LICENSE
   :alt: License

.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
   :target: https://github.com/psf/black
   :alt: Code style: black

This module provides various memoizing collections and decorators,
including variants of the Python Standard Library's `@lru_cache`_
function decorator.

.. code-block:: python

   from cachetools import cached, LRUCache, TTLCache

   # speed up calculating Fibonacci numbers with dynamic programming
   @cached(cache={})
   def fib(n):
       return n if n < 2 else fib(n - 1) + fib(n - 2)

   # cache least recently used Python Enhancement Proposals
   @cached(cache=LRUCache(maxsize=32))
   def get_pep(num):
       url = 'http://www.python.org/dev/peps/pep-%04d/' % num
       with urllib.request.urlopen(url) as s:
           return s.read()

   # cache weather data for no longer than ten minutes
   @cached(cache=TTLCache(maxsize=1024, ttl=600))
   def get_weather(place):
       return owm.weather_at_place(place).get_weather()

For the purpose of this module, a *cache* is a mutable_ mapping_ of a
fixed maximum size.  When the cache is full, i.e. by adding another
item the cache would exceed its maximum size, the cache must choose
which item(s) to discard based on a suitable `cache algorithm`_.  In
general, a cache's size is the total size of its items, and an item's
size is a property or function of its value, e.g. the result of
``sys.getsizeof(value)``.  For the trivial but common case that each
item counts as ``1``, a cache's size is equal to the number of its
items, or ``len(cache)``.

Multiple cache classes based on different caching algorithms are
implemented, and decorators for easily memoizing function and method
calls are provided, too.


Installation
------------------------------------------------------------------------

cachetools is available from PyPI_ and can be installed by running::

  pip install cachetools

Typing stubs for this package are provided by typeshed_ and can be
installed by running::

  pip install types-cachetools


Project Resources
------------------------------------------------------------------------

- `Documentation`_
- `Issue tracker`_
- `Source code`_
- `Change log`_


License
------------------------------------------------------------------------

Copyright (c) 2014-2021 Thomas Kemmer.

Licensed under the `MIT License`_.


.. _@lru_cache: https://docs.python.org/3/library/functools.html#functools.lru_cache
.. _mutable: https://docs.python.org/dev/glossary.html#term-mutable
.. _mapping: https://docs.python.org/dev/glossary.html#term-mapping
.. _cache algorithm: https://en.wikipedia.org/wiki/Cache_algorithms

.. _PyPI: https://pypi.org/project/cachetools/
.. _typeshed: https://github.com/python/typeshed/
.. _Documentation: https://cachetools.readthedocs.io/
.. _Issue tracker: https://github.com/tkem/cachetools/issues/
.. _Source code: https://github.com/tkem/cachetools/
.. _Change log: https://github.com/tkem/cachetools/blob/master/CHANGELOG.rst
.. _MIT License: https://raw.github.com/tkem/cachetools/master/LICENSE
