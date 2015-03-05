---
layout: documentation
title: Building cdec from source
---
This page gives a basic summary of how to acquire and build the `cdec` source code.  Before starting, you should be familiar with building and installing software on Unix-like platforms.

<hr/>
# Download the source code
You have two options for retrieving the code. The first (and simplest) option is to use a prepackaged source archive:

    wget http://demo.clab.cs.cmu.edu/cdec/cdec-{{site.current_version}}.tar.gz

<hr/>
# Configuring and compiling
Configuring and building the code looks *something* like this (depending on your system configuration and requirements, you may need to specify more options to `cmake`):

    cmake -G 'Unix Makefiles'
    make -j 4
    make test
    ./tests/run-system-tests.pl

<hr/>
# Third-party software dependencies
**You must have all the software in this section installed somewhere on your system!**

- [CMake](http://www.cmake.org/) build manager
- A C++ compiler **that supports the [C++11 standard](http://www.stroustrup.com/C++11FAQ.html)**, for example [gcc](http://gcc.gnu.org/) or [Clang](http://clang.llvm.org/).
- [Boost C++ libraries (version 1.44 or later)](http://www.boost.org/).
    - If you build your own boost, you _must install it_ using `bjam install` (this may require root access or configuring a nonstandard install location with `--prefix`).
    - Older versions of Boost may work, but problems have been reported on some platforms with older versions.
- [GNU Flex](http://flex.sourceforge.net/)
- [Python-2.7](http://docs.python.org/) is required to build the `pycdec` extensions (optional)
<hr/>
# Optional software extensions
The software in this section is optional. The extensions are configured with command line options to the `./configure` script prior to compilation.

<table>
<tr>
  <th style="width: 30%">Parameter</th>
  <th style="width: 80%">Description</th>
</tr>
<tr>
  <td><code>-DMETEOR_JAR=/path/to/meteor.jar</code></td>
  <td>Makes <a href="http://www.cs.cmu.edu/~alavie/METEOR/">METEOR</a> available for tuning and evaluation. You must specify the full path to the METEOR jar, and <code>java</code> must be available in your path.</td>
</tr>
<tr>
  <td><code>-DENABLE_MPI</code></td>
  <td><a href="http://www.mpi-forum.org/">MPI</a> can be used to parallelize some parameter optimization algorithms.</td>
</tr>
</table>
<br />

<hr/>
# Getting `cdec` from GitHub

If you intend to make changes to the `cdec` code, you will need to clone cdec from the central git repository, [which is hosted at github.](http://github.com/redpony/cdec) Checking out the code is simple enough:

    git clone git://github.com/redpony/cdec.git
    cd cdec

Prior to building the software for the first time, you must tell `cmake` to generate the project’s Makefiles for you.

    cmake -G 'Unix Makefiles'

<hr/>
# Building and installing Python extensions (optional)

    cd python
    python setup.py build
    python setup.py install

Note: the Python extensions must be installed somewhere Python will look for them by default. If you do not have access to Python's default library directory or do not wish to install cdec there, we recommend using [virtualenv](http://virtualenv.readthedocs.org)

<hr/>
# Supported Platforms

- Linux and Mac OS X are supported
- Windows is not supported (however, you may be able to get it to work)

