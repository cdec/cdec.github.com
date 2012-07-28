---
layout: documentation
title: Building cdec from source
---
This page gives a basic summary of how to acquire and build the cdec source code.  You should be familiar with building and installing software on Unix-like platforms before proceeding.

# Quick start
[Cdec is hosted at github.](http://github.com/redpony/cdec) Checking out the code and building it looks something like this:

    git clone git://github.com/redpony/cdec.git
    autoreconf -ifv
    ./configure \
          [--with-boost=/path/to/boost] \
          [--with-cmph=/path/to/cmph] \
          [--with-eigen=/path/to/eigen] \
          [--enable-mpi]
    make

# Third-party software dependencies

- [Git](http://git-scm.com/), for checking out software
- [boost c++ libraries version 1.44 or later](http://www.boost.org/).
    - If you build your own boost, you _must install it_ using `bjam install`.
- [Autoconf / Automake / Libtool](http://www.gnu.org/software/autoconf/) - configures the build environment.
    - Older versions of GNU autotools may not work properly.

# Optional software dependencies

- [libcmph-1.1](http://www.ark.cs.cmu.edu/cdyer/cmph-1.1-cdyer.tar.gz) is a perfect hashing function library that can be used to reduce the memory required to represented large numbers of features.
- [Eigen](http://eigen.tuxfamily.org) (optional linear algebra library, used for some experimental code)

# Platforms / compilers known to be compatible

- Linux on 64-bit platforms with gcc 4.1, 4.3, 4.4, 4.5, 4.6, 4.7
- MacOSX on Intel 32 bit with gcc 4.0, 4.5, on Intel 64 with gcc 4.6

There have been some reports of the code causing an Internal Compiler Error (ICE) in gcc 4.4 .

# Build issues on Mac OS X 10.4 and 10.5 with tr1/hashtable

Mac OS X 10.4 and 10.5 include a version of `g++` that contains a bug in one of the constructors of the STL's hashtable code.  To build cdec, you will need to fix this bug. Download the patched version of `tr1/hashtable` [here](http://openfst.cs.nyu.edu/twiki/bin/view/FST/CompilingOnMacOSX). The following assumes that the file was saved to `~/Downloads/hashtable`, replace that by the actual file location (note that your browser might have rename hashtable to hashtable.txt).
(Optional) Check how minimal the change is:

    diff  ~/Downloads/hashtable /usr/include/c++/4.0.0/tr1/hashtable

Overwrite Apple's version with the patched version and restore file permissions and ownership:

    sudo cp -f ~/Downloads/hashtable /usr/include/c++/4.0.0/tr1/hashtable
    sudo chmod 644 /usr/include/c++/4.0.0/tr1/hashtable
    sudo chown root:wheel /usr/include/c++/4.0.0/tr1/hashtable
