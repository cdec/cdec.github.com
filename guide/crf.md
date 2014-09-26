---
layout: documentation
title: cdec - Parameter learning
---

A conditional random field (CRF) is a log-[linear model](../concepts/linear-models.html) of a conditional (given input <span>\\( x \\)</span>) probability distribution over structured outputs <span>\\( \boldsymbol{y} \in \mathcal{Y}(x) \\)</span>. The [model parameters](../concepts/weights.html) in CRFs are trained to maximize the conditional log likelihood of a set of training data <span>\\( \left\\{ (x_i, \boldsymbol{y}_i) \right\\}^n \\)</span>.

In `cdec` every output is produced by some latent [derivation](../concepts/derivations.html). Moreover, any output <span>\\( \boldsymbol{y} \\)</span> will in general be derivable via many different *latent* derivations <span>\\( \boldsymbol{z} \in \mathcal{D}(x,\boldsymbol{y}) \\)</span> (note: the exact number of derivations depends on the ambiguity of the translation space entailed by the translation grammar and [translation formalism](../concepts/formalism.html); it is possible to construct grammars for some problems, like sequence labeling, that produce *unambiguous* derivations of every output).

Because outputs in `cdec` may be associated with many derivations, the probability of some output <span>\\( \boldsymbol{y} \\)</span> is defined to be the *marginal* probability, over all derivations that produce that output, <span>\\( p(\boldsymbol{y} \mid x) = \sum_{\boldsymbol{z} \in \mathcal{D}(x,\boldsymbol{y}) } p(\boldsymbol{z} \mid x) \\)</span>. Note that in the unambiguous case when there is just one derivation per output, this reduces to the standard CRF definition.

<hr/>
## Training CRFs with `cdec`

In contrast to most training objectives used in machine translation which attempt to maximize BLEU, CRFs training only "gives credit" to completely perfect outputs, all other outputs are considered "negative examples". Therefore, to use CRF training, your translation grammar must exactly be able to produce the reference translation. For some machine translation formalisms with heuristically learned translation rules (for example, [hiero](../concepts/hiero.html)), this is not always possible. But, for problems like part-of-speech tagging, where you are "translating" each word in the input into a sequence of NOUN, VERB, etc., it is not hard to guarantee that the output space will contain all possible labels.

<hr/>

## Further reading
* [Phil Blunsom, Trevor Cohn, and Miles Osborne. 2008. A Discriminative Latent Variable Model for Statistical Machine Translation. In *Proc. ACL*.](http://www.aclweb.org/anthology/P/P08/P08-1024.pdf)
* [Phil Blunsom and Miles Osborne. 2008. Probabilistic Inference for Machine Translation. In *Proc. EMNLP*.](http://aclweb.org/anthology-new/D/D08/D08-1023.pdf)
* [Fei Sha and Fernando Pereira. 2003. Shallow Parsing with Conditional Random Fields. In *Proc. ACL*.](http://www-bcf.usc.edu/~feisha/pubs/shallow03.pdf)
* [John D. Lafferty, Andrew McCallum, and Fernando Pereira. 2001. Conditional Random Fields: Probabilistic Models for Segmenting and Labeling Sequence Data. In *Proc. ICML*.](http://repository.upenn.edu/cgi/viewcontent.cgi?article=1162&context=cis_papers)
