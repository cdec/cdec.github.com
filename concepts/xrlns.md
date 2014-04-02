---
layout: documentation
title: Extended tree-to-string transducers
---
*Extended tree-to-string transducers* (xRn's) are a formalism that transduces between trees and strings. The variant we use are described in [this paper](http://www.cis.upenn.edu/~lhuang3/amta06-sdtedl.pdf) by [Liang Huang](http://acl.cs.qc.edu/~lhuang/) and colleauges. They support tree fragments of arbitrary depth on the source side and strings on the target side.

An example tree-to-string grammar, expressed in the cdec rule format is the following:

    (S [NP-C] [VP] (PUNC .)) ||| [1] [2] . ||| Rule1=1
    (NP-C (DT the) (NN gunman)) ||| qiangshou ||| Rule2=1
    (VP (VBD was) (VP-C [VBN] (PP (IN by) [NP-C]))) ||| bei [2] [1] ||| Rule3=1
    (NP-C (DT the) (NN police)) ||| jingfang ||| Rule4=1
    (VBN killed) ||| jibi ||| Rule5=1


