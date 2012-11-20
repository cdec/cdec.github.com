---
layout: documentation
title: Per-sentence grammars
---
Per-sentence grammars are [synchronous context-free grammars](/concepts/scfgs.html) filtered so as to contain just the rules necessary to translate a single sentence. They are loaded immediately before translation and unloaded when the translation process completes, which minimizes memory consumption.

# Marking up input to use per-sentence grammars

    <seg grammar="/home/cdec/grammar.125.scfg.gz"> Hier ist ein Satz . </seg>
    <seg grammar="/home/cdec/grammar.126.scfg.gz"> Ein anderer Satz ! </seg>

Per-sentence grammars must be in the [standard cdec grammar format](/documentation/grammar-format.html) and may optionally be compressed using `gzip`.

