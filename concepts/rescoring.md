---
layout: documentation
title: cdec - Feature functions
---
*Rescoring* is the process of applying a vector of [feature functions](feature_functions.html) and [feature weights](weights.html) to a set of translation candidate [derivations](derivations.html) so as to discriminate good from bad translations. Since rescoring functions may be *non-local* with respect to the primitive rules used in the translation model, rescoring may be computationally expensive, and require approximation algorithms, such as *cube pruning* for fast inference.

