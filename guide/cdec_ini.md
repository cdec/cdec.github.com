---
layout: documentation
title: cdec.ini
---

The `cdec.ini` file specifies the kind of [decoding algorithms](/concepts/formalism.html), [feature functions](/concepts/feature_functions.html), and [rescoring algorithms](/concepts/rescoring.html) that will be used.

An example configuration file for a large-scale SCFG system is shown here:
<pre>
formalism=scfg
add_pass_through_rules=true
feature_function=WordPenalty
feature_function=NonLatinCount
feature_function=KLanguageModel /usr1/home/lms/wmt2013-4gm.klm
feature_function=KLanguageModel -n ClassLM -m /usr1/home/lms/emitmap.txt.gz /usr1/home/lms/wmt2013-k600.klm
feature_function=RuleShape
cubepruning_pop_limit=1000
scfg_max_span_limit=18
</pre>

An example configuration for a tagger is shown here:
<pre>
formalism=tagger
tagger_tagset=/Users/cdyer/projects/tagging/en/tagset.txt
intersection_strategy=full
feature_function=LexicalPairIndicator
feature_function=NgramFeatures -o 3
</pre>

