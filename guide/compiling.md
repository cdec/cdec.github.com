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

# Building the Python extentions

    cd python
    python setup.py build

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
- [Python-2.7](http://docs.python.org/) is required to build the `pycdec` extensions

# Optional software dependencies
The software in this section is used to configure optional extensions.

<table border="1">
<col width="20%">
<col width="80%">
<tr>
  <td><b>Parameter</b></td>
  <td><b>Description</b></td>
</tr>
<tr>
  <td><code>--with-meteor</code></td>
  <td>Makes <a href="http://www.cs.cmu.edu/~alavie/METEOR/">METEOR</a> available for tuning and evaluation. You must specify the full path to the METEOR jar, and Java must be avialable in your path.</td>
</tr>
<tr>
  <td><code>--with-cmph</code></td>
  <td><a href="http://cmph.sourceforge.net/">libcmph-2.0</a> is a perfect hash function library that can be used to reduce the memory required to work with extremely large numbers of features.</td>
</tr>
<tr>
  <td><code>--enable-mpi</code></td>
  <td><a href="http://www.mpi-forum.org/">MPI</a> can be optionally used to parallelize some parameter optimization algorithms.</td>
</tr>
</table>
<br />

# Supported Platforms

- Linux and Mac OS X are supported
- Windows is not supported (however, you may be able to get it to work)

