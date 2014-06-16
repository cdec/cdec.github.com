---
layout: documentation
title: Extended tree-to-string transducers
---
*Extended tree-to-string transducers* (xRs's) are a formalism that transduces between trees and strings. The variant supported by `cdec` is described in [this paper](http://www.cis.upenn.edu/~lhuang3/amta06-sdtedl.pdf) by [Liang Huang](http://acl.cs.qc.edu/~lhuang/) and colleauges.

The tree transducers that are supported permit tree fragments of arbitrary depth on the source side (with an arbitrary number of non-terminal variables) to be paired with strings on the target side, which indicating a translational correspondence. Note: in contrast to the completely general tree-to-string formalism, deletion and copying of nonterminals is not supported (although adding support for these operations would not be terribly complicated), and the transducers only can have a single state.

An example tree-to-string rule table, expressed in the cdec rule format is the following:

    (S [NP-C] [VP] (PUNC .)) ||| [1] [2] . ||| Rule1=1 SomeOtherFeature=-2.37
    (NP-C (DT the) (NN gunman)) ||| qiāngshǒu ||| Rule2=1
    (VP (VBD was) (VP-C [VBN] (PP (IN by) [NP-C]))) ||| bèi [2] [1] ||| Rule3=1
    (NP-C (DT the) (NN police)) ||| jǐngfāng ||| Rule4=1
    (VBN killed) ||| jībì ||| Rule5=1

This set of rules will transduce the English input tree (in this formalism, inputs are phrase structure trees, not just sequences of words):

    (S (NP-C (DT the) (NN gunman)) (VP (VBD was) (VP-C (VBN killed) (PP (IN by) (NP-C (DT the) (NN police))))) (PUNC .))

into the Chinese output sentence

    qiāngshǒu bèi jǐngfāng jībì .

## Some remarks

 * Trees and tree fragments must be represented on a single line of text.
 * It is permitted to mix terminal and nonterminal symbols in productions rules (however, most parsers don't do this so it probably will never come up for you).
 * The minimal matchable unit is a non-terminal and its immediately dominated children (whether terminals, nonterminals, or a mix).

## Using tree-to-string translation with `cdec`

The tree-to-string backend for `cdec` is built automatically. To enable it in your translation project, you simply need to add the following lines in your `cdec.ini` file:

    formalism=t2s
    grammar=/path/to/rule-table.txt

Most users will also want to add self-transduction rules (so you can, e.g., handle inputs that contain words or syntactic structures that are not covered by the rules in the rule table). This can be added with the following:

    add_pass_through_rules=true

All of `cdec`'s rescoring, inference, and parameter learning functionality is available with the tree-to-string translation formalism.

## Extracting tree to string rules

Tree to string transduction rules can be extracted using the [HyperGrex tool](https://github.com/armatthews/HyperGrex), developed by [Austin Matthews](http://armatthews.com/). For your parsing needs, you might check out [Yue Zhang](http://www.sutd.edu.sg/yuezhang.aspx)'s [Zpar](http://www.sutd.edu.sg/cmsresource/faculty/yuezhang/zpar.html), which is fast and very good for Chinese.

