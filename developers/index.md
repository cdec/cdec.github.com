---
layout: documentation
title: cdec - Developers
---
# Developer documentation

cdec is [developed on Github](http://github.com/redpony/cdec) by [many volunteers](contributors.html) users are encouraged to fork us, develop the project further, and submit patches to the main project.

## Development guidelines
* Ensure that the system tests continue to function
* Adhere to the C++ style used in the rest of the decoder
* Do not add mandatory dependencies to third-party software

## Suggested projects
* Generic training framework: currently MERT, PRO, MinRisk, Rampion are seperate binaries that duplicate a great deal of functionality. This could be unified.
* Refactor the `DecoderImpl` object so that it does not have interface code. Rather, the `cdec` binary should be separate and interact with the `Decoder` library interface.
* Refactor decoder into smaller pieces: perhaps a Hypergraph library, a feature function library, translation/tagging library, and rescoring/inference library?

