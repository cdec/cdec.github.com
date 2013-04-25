---
layout: documentation
title: Sequence tagging
---
This page shows how to use [Conditional Random Field](http://en.wikipedia.org/wiki/Conditional_random_field) (CRF) models with `cdec` tools. CRF is a popular choice for modeling sequence tagging problems (e.g. part-of-speech tagging, named entity recognition, ...etc). We will use [POS tagging](http://en.wikipedia.org/wiki/Part-of-speech_tagging) as an example problem in this tutorial.

# [Build `cdec`]

# Problem
Given pairs of observation sequences and label sequences, train a CRF model to maximize the probability of each label sequence given the corresponding observation sequence. 

For example, in POS tagging, the observation sequence may look like:

    When  they  return  to  their   desks   at  1   p.m.  ,   they  have  pedaled   20  miles   .

while the label sequence may look like ([tagset](http://www.cst.dk/mulinco/filer/PennTreebankTS.html)):

    WRB   PRP   VBP     TO  PRP$    NNS     IN  CD  NN    ,   PRP   VBP   VBN       CD  NNS     .

After training the model, we would like to ask what is the best label sequences for a new observation sequence.

# Training data

Create a file with one training example per line. Each line should be formatted as follows: 

    o1 o2 o3 ... oN ||| l1 l2 l3 ... lN

For example, the previous sequence pair should be formatted as:

    When they return to their desks at 1 p.m. , they have pedaled 20 miles . ||| WRB PRP VBP TO PRP$ NNS IN CD NN , PRP VBP VBN CD NNS .

Example training data file can be found at https://github.com/cdec/cdec.github.com/blob/master/data/tb3.pos

# Grammar

Create a file to specify possible labels of a each observation. For example:

    [X] ||| return ||| VBP ||| F00=1
    [X] ||| return ||| NN ||| F00=1
    [X] ||| fish ||| VBP ||| F00=1
    [X] ||| fish ||| NN ||| F00=1
    [X] ||| fish ||| NNS ||| F00=1
    ...

Note: for better performance, try to use as few labels per observation as you could. For example, in the POS tagging problem, some words never appear with some labels in the training data. It's therefore recommended that you only add entries in the grammar for observation-label pairs which have been encountered in the training data.

Example grammar file can be found at https://github.com/cdec/cdec.github.com/blob/master/data/tb3.grammar

# Config file

formalism=scfg
intersection_strategy=full
grammar=/usr0/home/wammar/russian-mt-blitz-2013/transliterator/ruen/ruen.train.labels.pruned
scfg_max_span_limit=1
feature_function=NgramFeatures -o 2
feature_function=RuleContextFeatures -t F02|%x[-1]|%x[0]|%y[0]
feature_function=RuleContextFeatures -t F03|%x[0]|%x[1]|%y[0]

The `cdec` config file specifies:
- grammar formalism (for CRF, the formalism should always be set to 'scfg', short for Synchronous Context Free Grammar)
- intersection strategy (should be specified as 'full' for training the model, and should not be specified for decoding)
- grammar file
- maximum length of observation sequence which may correspond to a single label. For POS tagging, this should be set to 1 because tokens and POS tags should have one-to-one correspondence in a pair of an observation sequence and a label sequence.
- feature templates, defined over an observation sequence `x` and a label sequence `y`:
    - NgramFeatures -o NGRAM_ORDER: the number of times a label sequence of length NGRAM_ORDER appears in `y`
    - RuleContextFeatures -t TEMPLATE: you can think of TEMPLATE as a function of the observation sequence `x`, an index `i`, and the label `y[i]` which returns a string. The string is the feature ID, and the value is 1. For example, the template F02|%x[-1]|%x[0]|%y[0] fires the following features for the example given before `F02|<s>|When|WRB=1`, `F02|When|they|PRP=1`, `F02|they|return|VBP=1`, ...etc.
    
Notes: 
- Each rule in the grammar file is also used as a feature. Therefore, we do not need to add a RuleContextFeatures with template F04|%x[0]|%y[0] since it would have been redundant.
- Currently, RuleContextFeatures support templates which index any relative position in the observation sequence `x`, but it can only index the "current" label.

Example config file can be found at https://github.com/cdec/cdec.github.com/blob/master/data/tb3.train.ini

# Training

Each of the tools `$CDEC/training/crf/mpi_batch_optimize` and `$CDEC/training/crf/mpi_flex_optimize` can be used to train CRF models. The first performs batch optimization while the latter uses mini-batches. Type `mpi_batch_optimize --help` or `mpi_flex_optimize --help` to see their. Below is an example invocation which uses `mpi_flex_optimize` and specifies the mini-batch size to 10, number of iterations per mini-batch to 6, time-series regularization strength to 100, L2 regularization strength to 0.2, number of mini-batches to process to 600. 

    $CDEC/training/crf/mpi_flex_optimize \
      -d data/tb3.pos \
      -c data/tb3.train.ini \
      -s 10 -i 6 \
      -T 100 -C 0.2 -I 600

When it runs to completion, the current directory will contain a file weights.final.gz, which is a human-readable listing of all features and their corresponding weights.

Notes:
- mpi_flex_optimize usually converges faster.
- As their name suggests, both tools are mpi-friendly

# Decoding

After obtaining the optimized feature weights, we can ask `cdec` to find the most probable label sequence of a given observation sequence. The observation sequences are read from a file with one sequence per line. Observation items are space separated as follows:

    This is a new sentence .
    This is another one .
    ...

An example test file can be found at https://github.com/cdec/cdec.github.com/blob/master/data/tb3.test

An example invocation would be:

    $CDEC/decoder/cdec \
      -w weights.final.gz \
      -c data/tb3.test.ini \
      -i data/tb3.test

Notes:
- K-best label sequences can be found using the option `-k`. Use `cdec --help` for more details.

