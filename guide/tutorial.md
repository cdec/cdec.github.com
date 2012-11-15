---
layout: documentation
title: System building tutorial
---
This tutorial will guide you through the process of creating a Spanish-English statistical machine translation system with `cdec`. To complete this tutorial successfully, you will need:

 - About 1 hour of time
 - A Linux or MacOS X system with at least 2GB RAM
 - At least least 2GB disk space
 - Python 2.7 or newer

### 0. Prerequisites

 - [Compile `cdec`](compiling.html) and run `tests/run-system-tests.pl`
 - Build the `pycdec` Python language extensions to `cdec`
 - Download and compile [SRILM](http://www.speech.sri.com/projects/srilm/download.html) (for estimating the language model)
 - Download and untar [`cdec-spanish-demo.tar.gz`](http://data.cdec-decoder.org/cdec-spanish-demo.tar.gz) (16.7 MB)

### 1. Tokenize and lowercase the training, dev, and devtest data
Estimated time: **~2 minutes**
    ~/cdec/corpus/tokenize-anything.sh < training/news-commentary-v7.es-en |
       ~/cdec/corpus/lowercase.pl > nc.lc-tok.es-en

    ~/cdec/corpus/tokenize-anything.sh < dev/2010.es-en |
       ~/cdec/corpus/lowercase.pl > dev.lc-tok.es-en

    ~/cdec/corpus/tokenize-anything.sh < devtest/2011.es-en |
       ~/cdec/corpus/lowercase.pl > devtest.lc-tok.es-en

### 2. Filter training corpus sentence lengths
Estimated time: **20 seconds**.

    ~/cdec/corpus/filter-length.pl nc.lc-tok.es-en > training.es-en

### 3. Run word bidirectional word alignments
Estimated time: **~10 minutes**
    ~/cdec/training/fast_align -i training.es-en -d -v > training.es-en.fwd_align
    ~/cdec/training/fast_align -i training.es-en -d -v -r > training.es-en.rev_align

You can read more about [word alignment](/concepts/alignment.html) and the [`fast_align` alignment tool](fast_align.html).

### 4. Symmetrize word alignments
Estimated time: **5 seconds**
    ~/cdec/utils/atools -i training.es-en.fwd_align -j training.es-en.rev_align > training.gdfa

### 5. Compile the training data
Estimated time: **~1 minute**

*This step assumes your shell is `bash`*.

    export PYTHONPATH=`echo ~/cdec/python/build/lib.*`
    python -m cdec.sa.compile -b training.es-en -a training.gdfa -c extract.ini -o training.sa

### 6. Extract grammars for the dev and devtest sets
Estimated time: **15 minutes**

    python -m cdec.sa.extract -c extract.ini -g dev.grammars -j 2 < dev.lc-tok.es-en > dev.lc-tok.es-en.sgm
    python -m cdec.sa.extract -c extract.ini -g devtest.grammars -j 2 <
        devtest.lc-tok.es-en > devtest.lc-tok.es-en.sgm
The `-j 2` option tells the extractor to use 2 processors. This can be adjusted based on your hardward capabilities. The extraction process can be slow, so using more processors if they are available is recommended.

You can read more about the [synchronous context-free grammars](/concepts/scfgs.html) that are being extracted in this step.

### 7. Build the target language model
Estimated time: **1 minute**

    ~/cdec/corpus/cut-corpus.pl 2 training.es-en |
       ~/srilm/bin/i686/ngram-count -unk -text - -interpolate -kndiscount -lm nc.lm

You can read more about [language models](/concepts/language-models.html).

### 8. Compile the target language model
Estimated time: **5 seconds**

    ~/cdec/klm/lm/build_binary nc.lm nc.klm

### 9. Create a `cdec.ini` configuration file

Create a `cdec.ini` file with the following contents, making sure to substitute the full path to your language model for `$DEMO_ROOT`.
    formalism=scfg
    add_pass_through_rules=true
    density_prune=80
    feature_function=WordPenalty
    feature_function=KLanguageModel $DEMO_ROOT/nc.klm

Create a `weights.init` file (MERT requires that you list the features you want to optimize):
    CountEF 0.1
    EgivenFCoherent -0.1
    Glue 0.01
    IsSingletonF -0.01
    IsSingletonFE -0.01
    LanguageModel 0.1
    LanguageModel_OOV -1
    MaxLexFgivenE -0.1
    MaxLexEgivenF -0.1
    PassThrough -0.1
    SampleCountF -0.1

You can read more about [feature weights](/concepts/weights.html).

### 10. Tune system using development data with MERT
Estimated time: **20-40 minutes**

    ~/cdec/dpmert/dpmert.pl -w weights.init -d dev.lc-tok.es-en.sgm -c cdec.ini -j 2

The `-j 2` option tells MERT to use 2 processors for decoding and optimization. This can be adjusted based on your hardware capabilities.

You can read more about [linear models](/concepts/linear-models.html), [discriminative training](/concepts/training.html), and the [minimum error rate training algorithm](/documentation/mert.html).

### 11. Evaluate test set using trained weights
Estimated time: **5 minutes**

    ~/cdec/dpmert/decode-and-evaluate.pl -c cdec.ini -w dpmert/weights.final -i devtest.lc-tok.es-en.sgm -j 2


This will produce a score report that will look something like the following:
    ### SCORE REPORT #############################################################
      SCRIPT INPUT=devtest.lc-tok.es-en.sgm
            OUTPUT=eval.devtest.lc-tok.es-en.20121014-194914/test.trans
     DECODER INPUT=eval.devtest.lc-tok.es-en.20121014-194914/test.input
        REFERENCES=eval.devtest.lc-tok.es-en.20121014-194914/test.refs
    ------------------------------------------------------------------------------
              BLEU=0.273918
               TER=0.547938
    ##############################################################################

