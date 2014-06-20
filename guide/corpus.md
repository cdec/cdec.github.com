---
layout: documentation
title: Parallel corpora
---
Parallel data, such as that used for word alignment and grammar extraction, must be provided in text format where each line is a source language sentence (or phrase) and its target language translation, separated by a triple pipe symbol (`|||`). An example is as follows.

    doch jetzt ist der Held gefallen . ||| but now the hero has fallen .
    neue Modelle werden erprobt . ||| new models are being tested .
    doch fehlen uns neue Ressourcen . ||| but we lack new resources .

 - There may be only a single source sentence, but some tools will accept more than target language translation, which must be separated by a triple pipe.
 - Cdec is mostly encoding-agnostic, but some features expect UTF-8 encoded input.

## Preprocessing

Cdec provides basic corpus-preprocessing functionality including

 - tokenization using the `corpus/tokenize-anything.sh` script
 - lowercasing using the `corpus/lowercase.pl` script

## Multiple reference translations

Some applications can use multiple reference translations, these can be appended to each line, as follows:

    doch jetzt ist der Held gefallen . ||| but now the hero has fallen . ||| though now , the hero has fallen .
    neue Modelle werden erprobt . ||| new models are being tested . ||| new models are being checked .
    doch fehlen uns neue Ressourcen . ||| but we lack new resources . ||| however ,we are missing new resources .

