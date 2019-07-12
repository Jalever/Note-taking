---
layout: post
title: Introduction to Backtracking
subtitle: Backtracking Paradigm
date: 2019-07-03
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

- [Overview](#overview)
- [Description of the Method](#description-of-the-method)
- [Examples](#examples)

## Overview
Backtracking is a general algorithm for finding all (or some) solutions to some computational problems, notably <strong>Constraint Satisfaction Problem</strong>s, that incrementally builds candidates to the solutions, and abandons a candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution.

The classic textbook example of the use of backtracking is the <strong>Eight Queens Puzzle</strong>, that asks for all arrangements of eight chess queens on a standard chessboard so that no queen attacks any other. In the common backtracking approach, the partial candidates are arrangements of `k` queens in the first `k` rows of the board, all in different rows and columns. Any partial solution that contains two mutually attacking queens can be abandoned.

Backtracking can be applied only for problems which admit the concept of a "partial candidate solution" and a relatively quick test of whether it can possibly be completed to a valid solution. It is useless, for example, for locating a given value in an unordered table. When it is applicable, however, backtracking is often much faster than <strong>Brute Force</strong> enumeration of all complete candidates, since it can eliminate a large number of candidates with a single test.

Backtracking is an important tool for solving <strong>Constraint Satisfaction Problem</strong>s, such as <strong>Crossword</strong>s, <strong>Verbal Arithmetic</strong>, <strong>Sudoku</strong>, and many other puzzles. It is often the most convenient (if not the most efficient) technique for <strong>Parsing</strong>, for the <strong>Knapsack Problem</strong> and other combinatorial optimization problems. It is also the basis of the so-called Logic Programming Languages such as <strong>Icon</strong>, <strong>Planner</strong> and <strong>Prolog</strong>.

Backtracking depends on user-given "black box procedures" that define the problem to be solved, the nature of the partial candidates, and how they are extended into complete candidates. It is therefore a metaheuristic rather than a specific algorithm – although, unlike many other meta-heuristics, it is guaranteed to find all solutions to a finite problem in a bounded amount of time.

The term "backtrack" was coined by American mathematician <strong>D. H. Lehmer</strong> in the 1950s. The pioneer String-Processing language SNOBOL (1962) may have been the first to provide a built-in general backtracking facility.

## Description of the Method
The Backtracking algorithm enumerates a set of partial candidates that, in principle, could be completed in various ways to give all the possible solutions to the given problem. The completion is done incrementally, by a sequence of candidate extension steps.

Conceptually, the partial candidates are represented as the nodes of a tree structure, the potential search tree. Each partial candidate is the parent of the candidates that differ from it by a single extension step; the leaves of the tree are the partial candidates that cannot be extended any further.

The backtracking algorithm traverses this search tree recursively, from the root down, in depth-first order. At each `node c`, the algorithm checks whether `c` can be completed to a valid solution. If it cannot, the whole sub-tree rooted at `c` is skipped (pruned). Otherwise, the algorithm

1. checks whether `c` itself is a valid solution, and if so reports it to the user;
2. recursively enumerates all sub-trees of `c`.

The two tests and the children of each node are defined by user-given procedures.

Therefore, the actual search tree that is traversed by the algorithm is only a part of the potential tree. The total cost of the algorithm is the number of nodes of the actual tree times the cost of obtaining and processing each node. This fact should be considered when choosing the potential search tree and implementing the pruning test.

## Examples
Examples where backtracking can be used to solve puzzles or problems include:

- Puzzles such as <strong>Eight Queens Puzzle</strong>, <strong>Crossword</strong>s, <strong>Verbal Arithmetic</strong>, <strong>Sudoku</strong>, and <strong>Peg Solitaire</strong>.
- Combinatorial optimization problems such as <strong>Parsing</strong> and the <strong>Knapsack Problem</strong>.
- Logic Programming Languages such as <strong>Icon</strong>, <strong>Planner</strong> and <strong>Prolog</strong>, which use backtracking internally to generate answers.
