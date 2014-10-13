---
layout: documentation
title: cdec - Developers
---
# Developer documentation

cdec is [developed on Github](http://github.com/redpony/cdec) by [many volunteers](contributors.html) users are encouraged to fork us, develop the project further, and submit patches to the main project (general instructions on how to do so can be found [here](http://git-scm.com/book/ch5-2.html#Public-Small-Project)).

## Development guidelines
* Ensure that the system tests continue to function
* Adhere to the C++ style used in the rest of the decoder
* Do not add mandatory dependencies to third-party software

## Project ideas
* Support for variable length residual states in feature functions (rather than having the same sized residual state for all edges, let each edge decide how big the resulting state needs to be)
* Tree-to-tree translation (most of the functionality that is needed is present in the t2s translator; this is mostly a question of defining the text format of the t2t grammars)
* Get rid of pseudo-JSON serialization in favor of [Boost.Serialization](http://www.boost.org/doc/libs/1_56_0/libs/serialization/doc/index.html)
* Get rid of pseudo-MapReduce parallelization in MERT/PRO so the B64 code can be dropped
* Generic training framework: currently MERT, PRO, MinRisk, Rampion are seperate binaries that duplicate a great deal of functionality. This could be unified.
* Refactor the `DecoderImpl` object so that it does not have interface code. Rather, the `cdec` binary should be separate and interact with the `Decoder` library interface.
* Refactor decoder into smaller pieces: perhaps a Hypergraph library, a feature function library, translation/tagging library, and rescoring/inference library?

