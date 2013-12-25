---
layout: documentation
title: Lattices
---

A word lattice is a [directed acyclic graph](http://en.wikipedia.org/wiki/Directed_acyclic_graph) with a single start point and edges labeled with a word and weight. Unlike confusion networks which additionally impose the requirement that every path must pass through every node, word lattices can represent any finite set of strings. In general a word lattice can represent an exponential number of sentences in polynomial space. Here is an example lattice showing possible ways of splitting some compound words in German:
 
![Segmentation lattice example](/img/lattice.png)

## Representing lattice input

Lattices are encoded by ordering the nodes in a topological ordering and using this ordering to assign consecutive numerical IDs to the nodes. Then, proceeding in order through the nodes, each node lists its outgoing edges and the cost associated with them. For example, the above lattice can be written as:

    (
     (
      ('einen', 0, 1)
     ),
     (
      ('wettbewerbsbedingten', 0, 2),
      ('wettbewerbs', -0.2, 1),
      ('wettbewerb', -1.5, 1)
     ),
     (
      ('bedingten', 0, 1)
     ),
     (
      ('preissturz', 0, 2),
      ('preis', -2.0, 1)
     ),
     (
      ('sturz', -1.0, 1)
     )
    )

For each edge, the first field is a string representing the edge label, followed by a cost and the distance between the start and the end node of the edge. The string `'*EPS*'` indicates an espilon edge. This format is informally called the "Python lattice format" (PLF).

## Lattice translation

cdec accepts PLF lattices written on a single line as input. The edge cost value is associated with a feature weight named `LatticeCost`.

For more details on lattice translation, refer to:

Chris Dyer, Smaranda Muresan, and Philip Resnik. [Generalizing Word Lattice Translation](http://aclweb.org/anthology-new/P/P08/P08-1115.pdf). In _Proceedings of ACL 2008_.
