---
layout: documentation
title: Extended tree-to-string transducers
---
*Extended tree-to-string transducers* (xRn's) are a formalism that transduces between trees and strings. The variant we use are described in [this paper](http://www.cis.upenn.edu/~lhuang3/amta06-sdtedl.pdf) by [Liang Huang](http://acl.cs.qc.edu/~lhuang/) and colleauges. They support tree fragments of arbitrary depth on the source side (with an arbitrary number of non-terminal variables) and strings on the target side. Deletion and copying are not supported (although adding support for these operations would not be terribly complicated), and the transducers only can have a single state.

An example tree-to-string rule table, expressed in the cdec rule format is the following:

    (S [NP-C] [VP] (PUNC .)) ||| [1] [2] . ||| Rule1=1 SomeOtherFeature=-2.37
    (NP-C (DT the) (NN gunman)) ||| qiangshou ||| Rule2=1
    (VP (VBD was) (VP-C [VBN] (PP (IN by) [NP-C]))) ||| bei [2] [1] ||| Rule3=1
    (NP-C (DT the) (NN police)) ||| jingfang ||| Rule4=1
    (VBN killed) ||| jibi ||| Rule5=1

This set of rules will translate the input tree

    (S (NP-C (DT the) (NN gunman)) (VP (VBD was) (VP-C (VBN killed) (PP (IN by) (NP-C (DT the) (NN police))))) (PUNC .))

into the output sentence

    qiangshou bei jingfang jibi .

The tree-to-string formalism can be configured to be used by including the following line in your `cdec.ini` file:

    formalism=t2s
