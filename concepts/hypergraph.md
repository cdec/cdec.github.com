---
layout: documentation
title: Hypergraph
---
A *hypergraph* is a generalization of a graph such that a single edge may connect more than two nodes. The hypergraphs used in `cdec` are directed, acyclic, and every edge points to exactly one head node, but they may have zero or more tail nodes. Such hypergraphs are isomorphic to context-free grammars (in the same way that graphs are isomorphic to FSAs).
