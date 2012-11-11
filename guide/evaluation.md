---
layout: documentation
title: Evaluation
---
Evaluating the quality of a computer-generated translation relative to a human-generated reference translation or set of human-generated reference translations is useful for [automatic parameter tuning](/documentation/training.html), to compare the quality of two machine translation systems, and to carry out minimum Bayes risk decoding. The documentation on this page describes how `cdec` tools deal with evaluation and reference translations.

# Evaluation functions

`cdec` tools support the following translation evaluation functions:

 - [BLEU](http://acl.ldc.upenn.edu/P/P02/P02-1040.pdf) (native implementation)
 - [TER](http://mt-archive.info/AMTA-2006-Snover.pdf) (native implementation)
 - [METEOR](http://www.cs.cmu.edu/~alavie/METEOR/pdf/meteor-wmt11.pdf) (requires [supplementary software](http://www.cs.cmu.edu/~alavie/METEOR/))
 - CER (character edit rate; native implemtation)
 - Linear combinations of the above

# Reference format

Multiple references for each sentence can be represented in a single text file by separating the different translations by a triple pipe (`|||`) character. Different lines may have different numbers of references.

    This is reference #1 ||| This is alternative reference #1 ||| Here is another reference #1
    Reference 2 is on the second line ||| Reference 2 is located on line 2 ||| Second reference, second line
    And so forth ||| etc. ||| et cetera ...

# Evaluating translation output

By default, BLEU is used for evaluation:
    ./mteval/fast_score -r references.txt -i hypothesis.txt

Here is another option:    
    ./mteval/fast_score -r references.txt -i hypothesis.txt -m ter

# Adding evaluation functions

There are two mechanisms for adding evaluation functions to `cdec`. These will then be available for parameter tuning, minimum Bayes risk rescoring, and output scoring.

 - Implement the `EvaluationMetric` interface (see [`ns.h`](https://github.com/redpony/cdec/blob/master/mteval/ns.h)) may be overridden.
 - Implement software that implements the [text evaluation protocol](https://github.com/redpony/cdec/blob/master/mteval/README.protocol)

