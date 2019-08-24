.. image:: https://circleci.com/gh/surfertas/CppLocalization.svg?style=svg
    :target: https://circleci.com/gh/surfertas/CppLocalization

CppLocalization: filters and slam algorithms implemented in C++
========
This is a WIP C++ implementation of the filterpy_ library.

.. _filterpy: https://github.com/rlabbe/filterpy

Filters:

- `Unscented Kalman Filter`_

.. _Unscented Kalman Filter: https://github.com/surfertas/CppLocalization/blob/master/src/unscented_kalman_filter.cpp

Setup
----------

.. code:: bash

  mkdir build && cd build
  cmake ..
  make

Contribute
----------

- Style Guide: github.com/lefticus/cppbestpractices/blob/master/03-Style.md

Support
-------

If you are having issues, please let me know at tasuku {at} gmail.com

License
-------

The project is licensed under the MIT license.
