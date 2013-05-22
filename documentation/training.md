---
layout: documentation
title: cdec - Parameter learning
---

`cdec` includes implementations of the following discriminative parameter learning algorithms. Except for conditional likelihood training, other algorithms make use of an [evaluation function](/guide/evaluation.html).

* __[Dynamic Programming MERT (Kumar et al., 2009)](mert.html)__
    * Optimal for small numbers of features
    * Target any automatic translation metric
    * Distributed decoding for batch weight updates
* __[Rampion (Gimpel and Smith, 2012)](rampion.html)__
    * Target any sentence-decomposible automatic translation metric
    * L2 regularization
    * Distributed decoding for batch weight updates
* __[PRO (Hopkins and May, 2011)](pro.html)__
    * Target any sentence-decomposible automatic translation metric
    * L1 and L2 regularization
    * Distributed decoding for batch weight updates
* __[Dtrain (Simianer et al., 2012)](dtrain.html)__
    * Large-scale discriminative learning and feature selection
    * Distributed with MapReduce
    * Optimized for very large training sets
* __[Maximum Conditional Likelihood Training (Blunsom et al., 2008)](crf.html)__
    * Marginalize latent derivation variables
    * Online, batch, and minibatch variants
    * Optimized for very large numbers of features and/or large training sets
    * L1 and L2 regularization
    * Distributed inference with MPI
* __[Minimum Risk Training (Smith and Eisner, 2005)](minrisk.html)__
    * Target any sentence-decomposible automatic translation metric
    * L1, L2, and entropy regularization
    * Distributed decoding for batch weight updates
* __[MIRA (Chiang et al., 2008)](mira.html)__
    * Target any sentence-decomposible automatic translation metric
    * Single core, online algorithm only
    * No support for regularization

## Development ideas
* Although these algorithms are similar in structure and function, each uses a separate driver program. Since these independent driver programs have a fair amount of duplicated logic (e.g., for managing decoding workflow and the distribution of weights across iterations), a single driver program could conceivably be used for all or many of them.

