---
layout: documentation
title: cdec - Feature functions
---
*Feature functions* are functions <span>\\( f : \textbf{f},\textbf{e},\textbf{d} \mapsto \mathbb{R} \\)</span> that compute real-valued (possibly multi-dimensional) features of source sentences (<span>\\( \textbf{f} \\)), target language translations (<span>\\( \textbf{e} \\)), and their [translation derivation](derivations.html) (<span>\\( \textbf{d} \\)) to determine if a particular translation hypothesis is good or bad. Each feature is associated with a real-valued [weight](weights.html) in the [linear translation model](linear-models.html).

Example features:

 - target language model log probability
 - generative translation model log probability
 - target word count

# Feature locality and context dependence
The key to doing efficient prediction with translation models is using features that decompose additively over small pieces of the translation derivation. For example, a generative translation model probability is defined to be the product of the probabilities of several conditionally independent events. In log space, these quantities add, and thus a feature that is the translation model probability can be formulated as the sum of several **local features**.

### Source context dependence

 - **Context independent features** have the same value locally regardless of the source language context that the structure occurs in.
 - **Context dependent features** will have different values depending on the source language context.

### Non-local features

