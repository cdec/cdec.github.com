---
layout: documentation
title: Building cdec from source
---
This page gives a basic summary of how to acquire and build the `cdec` source code.  Before starting, you should be familiar with building and installing software on Unix-like platforms.

# Quick start
[Cdec is hosted at github.](http://github.com/redpony/cdec) Checking out the code and building it looks *something* like this (in particular, you may need to specify more options to `./configure`):

    git clone git://github.com/redpony/cdec.git
    cd cdec
    autoreconf -ifv
    ./configure [--with-boost=/path/to/boost-install]
    make
    ./tests/run-system-tests.pl

# Third-party software dependencies
**You must have all the software in this section installed somewhere on your system!**

- [Git](http://git-scm.com/), to check out the source code
- [Autoconf / Automake / Libtool](http://www.gnu.org/software/autoconf/) - is used to configure the build environment.
    - Older versions of GNU autotools may not work properly.
- A relatively recent version of a C++ compiler, for example [gcc](http://gcc.gnu.org/).
- [Boost C++ libraries (version 1.44 or later)](http://www.boost.org/).
    - If you build your own boost, you _must install it_ using `bjam install`.
    - Older versions of Boost may work, but problems have been reported on some platforms with older versions.
- [GNU Flex](http://flex.sourceforge.net/)

# Optional software dependencies
The software in this section is used to configure optional extensions.

- [Python-2.7](http://docs.python.org/) is required to build the `pycdec` extensions
- [libcmph-2.0](http://cmph.sourceforge.net/) is a perfect hashing function library that can be used to reduce the memory required to represented large numbers of features.
- [Eigen](http://eigen.tuxfamily.org) is a linear algebra library that is used for some experimental code
- [MPI](http://www.mpi-forum.org/) is optionally used for some training algorithms

# Supported Platforms
- Linux and Mac OS X are supported
- Windows is not supported (however, you may be able to get it to work)

