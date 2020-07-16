---
title: Complexity
nav_order: 0
---

Beyond whether or not a program is correct, computer scientists are often concerned about the **complexity** of a program. We actually already have quite a bit of experience with one particular kind of complexity that arises from how we design abstractions for our programs. For instance, pulling repeated code out into a method gives it a name and makes it easier for the reader to understand the behavior of the program. **Cognitive complexity** is about how easy it is to understand a program.

Code is just one way for programmers to communicate ideas to others, and writing code requires worrying about cognitive complexity. But programmers also communicate ideas to others in terms of **algorithms**, the more generalizable list of steps behind the code. Whereas code is specific to a particular programming language, we can communicate algorithms in natural languages like English too. Whenever we're describing a program to someone else, we're really describing an algorithm.

Today, we'll study one metric for algorithm analysis: **time complexity**, or how long it takes for an algorithm to evaluate.
