---
layout: documentation
title: cdec - Parameter learning
---

A conditional random field (CRF) is a log-[linear model](../concepts/linear-models.html) of a conditional (given input <span>\\( x \\)</span>) probability distribution over structured outputs <span>\\( \boldsymbol{y} \in \mathcal{Y}(x) \\)</span>. CRFs are trained to maximize the conditional log likelihood of a set of training data by setting the [weights](../concepts/weights.html) appropriately. To prevent overfitting, a prior on norm of the weight vector is often used that encourages, e.g., small or sparse vectors.

In contrast to most toolkits for learning CRFs, in `cdec` there may be many different latent *derivations* that produce a particular output <span>\\( \boldsymbol{y} \\)</span>.

<hr/>


## Further reading
* [Phil Blunsom, Trevor Cohn, and Miles Osborne. 2008. A Discriminative Latent Variable Model for Statistical Machine Translation. In *Proc. ACL*.](http://www.aclweb.org/anthology/P/P08/P08-1024.pdf)
* [Phil Blunsom and Miles Osborne. 2008. Probabilistic Inference for Machine Translation. In *Proc. EMNLP*.](http://aclweb.org/anthology-new/D/D08/D08-1023.pdf)
# [Fei Sha and Fernando Pereira. 2003. Shallow Parsing with Conditional Random Fields. In *Proc. ACL*.](http://www-bcf.usc.edu/~feisha/pubs/shallow03.pdf)
# [John D. Lafferty, Andrew McCallum, and Fernando Pereira. 2001. Conditional Random Fields: Probabilistic Models for Segmenting and Labeling Sequence Data. In *Proc. ICML*.](http://repository.upenn.edu/cgi/viewcontent.cgi?article=1162&context=cis_papers)

