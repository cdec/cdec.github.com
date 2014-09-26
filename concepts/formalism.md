---
layout: documentation
title: cdec - Translation formalisms
---
Translation formalisms are the set of computational primitives that constrain how a translation model will be able to transform an input into an output. `cdec` supports a number of different formalisms (primarily various kinds of [synchronous context-free grammars (SCFGs)](scfgs.html) and [finite-state transducers](fsts.html)), and these must be configured in the [decoder configuration file](/guide/cdec_ini.html) using the `formalism` keyword.

<hr />
## Supported formalism keywords

* `scfg` - this formalism translates sentences or lattices using a synchronous context-free grammar (SCFG).
* `tagger` - this formalism labels a sentence from a finite set of tags, where every tag is available to tag every word.
* `t2s` - this formalism transduces a context free tree into a string using [tree-to-string transducers](xrs.html).
* `rescore` - this formalism is used for rescoring a hypergraph of alternative strings.
* `fst` - this formalism translates a set of strings encoded as a context-free grammar (CFG) using a weighted finite state transducer.

## Experimental or internal formalism keywords

* `pb`
* `t2t`
* `csplit`
* `lextrans`
* `lexalign`

