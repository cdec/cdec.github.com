---
layout: documentation
title: cdec - k-best format
---

Generating *k*-best lists translation hypotheses is useful in a variety of situations. To produce them, you can invoke the decoder with the `-k N` option. Use the `-r` option to obtain **unique** *k*-best lists (duplicate entries may be contained in default lists on account of derivational ambiguity).

*k*-best lists contain a variety of information about the translation, with fields separated by a triple pipe symbol (`|||`):

![Alignment Example](/img/kbest.png)

