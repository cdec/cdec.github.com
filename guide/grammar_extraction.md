---
layout: documentation
title: Grammar extraction
---
Grammar extraction is the process of building a [translation grammar](scfgs.html) from a [word-aligned](alignment.html) parallel corpus. Unlike other translation systems, `cdec` recommends using [per-sentence grammars](psgs.html), i.e., grammars are constructed that are filtered for each sentence that is going to be translated.

