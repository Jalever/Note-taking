---
layout: post
title: Introduction to Dynamic Programming
subtitle: Dynamic Programming Paradigm
date: 2019-07-01
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

## Overview
<strong>Dynamic Programming</strong> is both a <strong>Mathematical Optimization Method</strong> and a <strong>Computer Programming Method</strong>. The method was developed by <ins>Richard Bellman</ins> in the 1950s and has found applications in numerous fields, from <strong>Aerospace Engineering</strong> to <strong>Economics</strong>. `In both contexts it refers to simplifying a complicated problem by breaking it down into simpler sub-problems in a recursive manner`. While some decision problems cannot be taken apart this way, decisions that span several points in time do often break apart recursively. Likewise, in <strong>Computer Science</strong>, if a problem can be solved optimally by breaking it into sub-problems and then recursively finding the optimal solutions to the sub-problems, then it is said to have optimal substructure.

If sub-problems can be nested recursively inside larger problems, so that <strong>Dynamic Programming Methods</strong> are applicable, then there is a relation between the value of the larger problem and the values of the sub-problems. In the optimization literature this relationship is called the <strong>Bellman Equation</strong>.

#### Computer Programming
There are two key attributes that a problem must have in order for <strong>Dynamic Programming</strong> to be applicable: <strong>Optimal Substructure</strong> and <strong>Overlapping Sub-problems</strong>. If a problem can be solved by combining optimal solutions to non-overlapping sub-problems, the strategy is called <strong>Divide and Conquer</strong> instead. This is why <strong>Merge Sort</strong> and <strong>Quick Sort</strong> are not classified as <strong>Dynamic Programming Problem</strong>s.

<strong>Optimal Substructure</strong> means that the solution to a given optimization problem can be obtained by the combination of optimal solutions to its sub-problems. Such Optimal Substructures are usually described by means of recursion. For example, given a graph `G=(V,E)`, the shortest path `p` from a vertex `u` to a vertex `v` exhibits optimal substructure: take any intermediate vertex `w` on this shortest path `p`. If `p` is truly the shortest path, then it can be split into sub-paths `p1` from `u` to `w` and `p2` from `w` to `v` such that these, in turn, are indeed the shortest paths between the corresponding vertices. Hence, one can easily formulate the solution for finding shortest paths in a recursive manner, which is what the <strong>Bellman–Ford Algorithm</strong> or the <strong>Floyd–Warshall Algorithm</strong> does.

<strong>Overlapping Sub-problem</strong>s means that the space of sub-problems must be small, that is, any recursive algorithm solving the problem should solve the same sub-problems over and over, rather than generating new sub-problems. For example, consider the recursive formulation for generating the `Fibonacci` series: `Fi = Fi−1 + Fi−2`, with base case `F1 = F2 = 1`. Then `F43 = F42 + F41`, and `F42 = F41 + F40`. Now `F41` is being solved in the recursive sub-trees of both `F43` as well as `F42`. Even though the total number of sub-problems is actually small (only 43 of them), we end up solving the same problems over and over if we adopt a naive recursive solution such as this. <strong>Dynamic Programming</strong> takes account of this fact and solves each sub-problem only once.

This can be achieved in either of two ways:

<strong>Top-Down Approach</strong>: This is the direct fall-out of the recursive formulation of any problem. If the solution to any problem can be formulated recursively using the solution to its sub-problems, and if its sub-problems are overlapping, then one can easily memoize or store the solutions to the sub-problems in a table. Whenever we attempt to solve a new sub-problem, we first check the table to see if it is already solved. If a solution has been recorded, we can use it directly, otherwise we solve the sub-problem and add its solution to the table.

<strong>Bottom-Up Approach</strong>: Once we formulate the solution to a problem recursively as in terms of its sub-problems, we can try reformulating the problem in a bottom-up fashion: try solving the sub-problems first and use their solutions to build-on and arrive at solutions to bigger sub-problems. This is also usually done in a tabular form by iteratively generating solutions to bigger and bigger sub-problems by using the solutions to small sub-problems. For example, if we already know the values of `F41` and `F40`, we can directly calculate the value of `F42`.

## Examples
#### Dijkstra algorithm for the Shortest Path Problem
From a Dynamic Programming point of view, Dijkstra's Algorithm for the Shortest Path Problem is a successive approximation scheme that solves the dynamic programming functional equation for the shortest path problem by the Reaching method.

In fact, Dijkstra's explanation of the logic behind the algorithm, namely

Find the path of minimum total length between two given nodes `P` and `Q`.

"We use the fact that, if `R` is a node on the minimal path from `P` to `Q`, knowledge of the latter implies the knowledge of the minimal path from `P` to `R`"

is a paraphrasing of Bellman's famous <strong>Principle of Optimality</strong> in the context of the Shortest Path Problem.

#### Fibonacci Sequence
Here is a naive implementation of a function finding the `nth` member of the Fibonacci Sequence, based directly on the mathematical definition:
![Z7Udr6.png](https://s2.ax1x.com/2019/07/16/Z7Udr6.png)

Notice that if we call, say, `fib(5)`, we produce a call tree that calls the function on the same value many different times:
![Z7UrIe.png](https://s2.ax1x.com/2019/07/16/Z7UrIe.png)

In particular, `fib(2)` was calculated three times from scratch. In larger examples, many more values of `fib`, or <ins>Subproblem</ins>s, are <ins>Recalculated</ins>, leading to an exponential time algorithm.

Now, suppose we have a simple <strong>Map</strong> object, <strong>m</strong>, which maps each value of `fib` that has already been calculated to its result, and we modify our function to use it and update it. The resulting function requires only `O(n)` time instead of exponential time (but requires `O(n)` space):
![Z7UXLV.png](https://s2.ax1x.com/2019/07/16/Z7UXLV.png)

This technique of saving values that have already been calculated is called <strong>Memoization</strong>; this is the <strong>Top-Down Approach</strong>, since we first break the problem into subproblems and then calculate and store values.

In the <strong>Bottom-Up Approach</strong>, we calculate the smaller values of `fib` first, then build larger values from them. This method also uses `O(n)` time since it contains a loop that repeats `n − 1` times, but it only takes constant `O(1)` space, in contrast to the top-down approach which requires `O(n)` space to store the map.
![Z7aQSA.png](https://s2.ax1x.com/2019/07/16/Z7aQSA.png)

In both examples, we only calculate `fib(2)` one time, and then use it to calculate both `fib(4)` and `fib(3)`, instead of computing it every time either of them is evaluated.
