---
layout: documentation
title: cdec - Rescoring external hypergraphs
---
`cdec` implements a large number of [feature functions](feature_functions.html) that can be useful for distinguishing well-formed strings from poorly formed strings. If you have another tool that generates hypergraphs (i.e., context-free structured string sets), you can read this in with cdec, and use its rescoring functionality, including parameter estimation.

There is a tool `training/tools/convert_grammar` that will read in a text-formatted context-free grammar representing your hypergraph and convert it into a `cdec` hypergraph. **Note**: you can only rescore CFGs that define a finite language.

An example of the text format is as follows:

    [S] ||| [S1]
    [S1] ||| [NP1] [VP] ||| Active=1
    [VP] ||| [V] [NP2]
    [V] ||| ate
    [VPSV] ||| was eaten
    [S1] ||| [NP2] [VPSV] by [NP1] ||| Passive=1
    [NP1] ||| John
    [NP2] ||| broccoli
    [NP2] ||| the broccoli ||| Definite=1

This is similar to the format used by [synchronous context-free grammars](scfgs.html).

You can read this in to `cdec` and make it available for rescoring (parameter learning, etc.) with the following command:

    cat input.cfg | ./training/utils/grammar_convert | ./decoder/cdec -f rescore

For example, using the `-k 1000` option to show the *k*-best derivations produces the following output:

    0 ||| John ate broccoli ||| Active=1 ||| 0
    0 ||| broccoli was eaten by John ||| Passive=1 ||| 0
    0 ||| John ate the broccoli ||| Active=1 Definite=1 ||| 0
    0 ||| the broccoli was eaten by John ||| Passive=1 Definite=1 ||| 0

