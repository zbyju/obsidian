Attribute translation CFG
Semantic evaluations in syntax-directed translation

every symbol (non-terminal, terminal, output symbol) of a CFG can have an attribute

an attribute x of a symbol A is written A.x (dot notation)
that the values of attributes are defined by attribute (semantic) rules
each semantic rule is associated with just one syntactic rule

2 types of attributes:
1. Synthesized
2. Inherited

Example:

Syntax:
1. S^0 -> aS^1b
2. S -> eps

Semantics:
1. S^0.n = S^1.n + 1
2. S.n = 0 (in the subtree of such S, there is 0 times 'a')

Generally:
1. Synthesized S -> aAb | S.s = f()

