---
layout: documentation
title: Translation derivations
---
A *translation derivation* is the set of rules and the order they were applied in to produce a translation of some input, and every output produced by cdec is associated with a derivation. While a single output string may be associated with any number of different derivations, which may in turn have different scores, every derivation will produce just a single output. The set of derivations is compactly represented in `cdec` as a [hypergraph](hypergraph.html).

