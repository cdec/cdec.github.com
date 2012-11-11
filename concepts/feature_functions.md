---
layout: documentation
title: cdec - Feature functions
---
*Feature functions* compute real-valued features of translation derivations that are used to determine if a particular translation hypothesis is good or bad. Each feature is associated with a real-valued [weight](weights.html) in the [linear translation model](linear-models.html).

Example features include target language model log probabilities, translation probabilities, and word and phrase count features.

# Feature locality
Features my be classified by whether they are *local* and whether they depend on the source language *context* they occur in.

 - *Local features* decompose linearly over the rules used in the translation with values depending only on the input and the translation rules.
 - *Non-local features* depend on more than one translation rule.

 - *Context independent features* have the same value regardless of the context that a rule is used in
 - *Context dependent features* are not conditionally independent of the input, given the rules used in translation.


