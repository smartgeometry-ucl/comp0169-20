---
title: Recursion
nav_order: 0
---

Throughout the course so far, we've seen that the choice of **data abstraction** affects how we solve programming problems. For example, we learned about certain templates for solving list problems, stack problems, queue problems: each of which required us to engage differently with how we organize code to manipulate data in a program.

For the remaining half of the course, we'll study an equivalent paradigm shift in the context of **functional abstraction**. Earlier, we presented a narrow definition of functional abstraction focusing on the relationship between client and implementer.

> The `Balance` class defines public methods so that other programs written by anyone, anywhere, at anytime before or after it can rely on its functionality as long as they know how to interface with it.

A more general definition for functional abstraction considers all **algorithms** in terms of three components.

1. All algorithms take parameters as input.
1. All algorithms perform computation with the given parameters.
1. All algorithms return results based on the computations.

**Recursive algorithms** represent a style of solving problems by combining solutions to smaller subproblems.

1. Recursive algorithms take parameters as input.
1. Recursive algorithms perform computation with the given parameters.
   1. Identify smaller **subproblems** that can be solved independently.
   1. Solve each smaller subproblem with **recursive calls**.
   1. Combine the result of each subproblem to compute the complete result.
1. Recursive algorithms return results based on the computations.

It turns out that we (as humans) use recursion in everyday English. English sentences allow syntactic recursion with phrases embedded within phrases.[^1]

[^1]: Edward Gibson. 9.59J Lab in Psycholinguistics. Spring 2017. Massachusetts Institute of Technology: MIT OpenCourseWare, <https://ocw.mit.edu>. License: [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/).

Conjunction
: [[John and Mary] and Bill]

Clausal complements
: [John thinks that [Mary said that [the girl cried]]]

Possessives
: [[[[John]'s mother]'s brother]'s house]
: [the house of [the brother of [the mother of [John]]]]

> In syntactocentric linguistics, **recursive syntax** (embedding phrases within phrases) has been hypothesized to be the critical feature of human language capacity. Although this claim has been challenged in recent decades, generating understandable human language remains a key challenge for computer programming given the infinite expressiveness of human language. Can we define a program to generate all possible English sentences?

Recursive algorithms present one direct approach for answering this question. But before we try to tackle that question, we'll study recursive algorithms for problems that we already know how to solve in order to build a foundation for answering these bigger questions in the future.
