---
layout: documentation
title: cdec - Translation formalisms
---
Translation formalisms are the set of computational primitives that constrain how a translation model will be able to transform an input into an output. `cdec` supports a number of different formalisms (primarily various kinds of [synchronous context-free grammars (SCFGs)](scfgs.html) and [finite-state transducers](fsts.html)), and these must be configured in the [decoder configuration file](/guide/cdec_ini.html) using the `formalism` keyword.
