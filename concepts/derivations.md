---
layout: documentation
title: Translation derivations
---
A *translation derivation* is the set of rules and the order they were applied in to produce a translation of some input, and every output produced by cdec is associated with a derivation. While a single output string may be associated with any number of different derivations, which may in turn have different scores, every derivation will produce just a single output. The set of derivations for an input <span>\\( x \\)</span> will be written as <span>\\( \mathcal{D}(x) \\)</span> in this documentation. The data structure used to represent this set in `cdec` is a [hypergraph](hypergraph.html).

## Translation forest

The set of all translations of an input <span>\\( x \\)</span> is a set of derivations <span>\\( \mathcal{D}(x) \\)</span>.

## Alignment forest

`cdec` can also compute the set of all derivations that produce a particular output string <span>\\( \boldsymbol{y} \\)</span> given an input <span>\\( x \\)</span>. This set is designated <span>\\( \mathcal{D}(x,\boldsymbol{y}) \\)</span>.

