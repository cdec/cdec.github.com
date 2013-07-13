---
layout: documentation
title: Building cdec from source
---
This page gives a basic summary of how to acquire and build the `cdec` source code.  Before starting, you should be familiar with building and installing software on Unix-like platforms.

# Download the source code
You have two options for retrieving the code. The first (and simplest) option is to use a prepackaged source archive:

    wget http://demo.clab.cs.cmu.edu/cdec/cdec-2013-07-13.tar.gz

# Configuring and compiling
Configuring and building the code looks *something* like this (depending on your system configuration and requirements, you may need to specify more options to `./configure`):

    ./configure [--with-boost=/path/to/boost-install]
    make
    ./tests/run-system-tests.pl

# Building the Python extentions

    cd python
    python setup.py build

# Third-party software dependencies
**You must have all the software in this section installed somewhere on your system!**

- A relatively recent version of a C++ compiler, for example [gcc](http://gcc.gnu.org/).
- [Boost C++ libraries (version 1.44 or later)](http://www.boost.org/).
    - If you build your own boost, you _must install it_ using `bjam install`.
    - Older versions of Boost may work, but problems have been reported on some platforms with older versions.
- [GNU Flex](http://flex.sourceforge.net/)
- [Python-2.7](http://docs.python.org/) is required to build the `pycdec` extensions

# Optional extensions
The software in this section is optional. The extensions are configured with command line options to the `./configure` script prior to compilation.

<table>
<tr>
  <th style="width: 20%">Parameter</th>
  <th style="width: 80%">Description</th>
</tr>
<tr>
  <td><code>--with-meteor</code></td>
  <td>Makes <a href="http://www.cs.cmu.edu/~alavie/METEOR/">METEOR</a> available for tuning and evaluation. You must specify the full path to the METEOR jar, and Java must be available in your path.</td>
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

# Getting `cdec` from GitHub

If you intend to make changes to the `cdec` code, you will need to clone cdec from the central git repository, [which is hosted at github.](http://github.com/redpony/cdec) Checking out the code is simple enough:

    git clone git://github.com/redpony/cdec.git
    cd cdec

Prior to building the software for the first time, or when you make certain kinds of changes (such as adding new files), you will need to generate the configuration and make scripts. Doing this requires recent versions of [Autoconf](http://www.gnu.org/software/autoconf/), [Automake](http://www.gnu.org/software/automake/), and [Libtool](http://www.gnu.org/software/libtool/).

    autoreconf -ifv

# Supported Platforms

- Linux and Mac OS X are supported
- Windows is not supported (however, you may be able to get it to work)

