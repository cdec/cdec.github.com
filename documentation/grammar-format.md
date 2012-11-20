---
layout: documentation
title: cdec - Rule format
---

The following illustrates the text encoding of a [SCFG](/concepts/scfgs.html) consisting of two rewrite rules:

![Rule format](/img/rulefile.png)

This text file consists of the following fields, separated by a triple pipe symbol (`|||`):

 - The **left-hand side (LHS)** is the nonterminal category that the rule rewrites as.
 - The **source language right-hand side (RHS)** is the string of source language terminal symbols and **nonterminal variables**. Nonterminal variables are surrounded by square brackets and contain only numbers and uppercase letters; e.g., `[X]`, `[NT]`, `[SBAR]`, or `[VP]`.  It is not necessary to provide an source nonterminal variable indices since they may only be indexed 1, 2, 3...
 - The **target RHS** is the sequence of target language terminal symbols and **nonterminal references**. Nonterminal references indicate correspondences to nonterminal symbols in the source side and are designated by the 1-based index of the source nonterminal, for example `[1]` and `[2]`. It is not necessary to specify the source nonterminal type since this is determined by the reference.
 - The **features** of a rule are a list of key-value pairs. Any derivation that uses this rule will have these feature vector added to its derivation feature vector.
 - *Optional*. The **terminal alignments** indicate the internal word alignments of the terminal symbols in the source and target languages. These may be useful for computing some feature values at run time.

## Source code

Data structures for representing individual rules are defined in `decoder/trule.h`.



