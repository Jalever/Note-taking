---
layout: post
title: Introduction to Divide and Conquer Algorithm
subtitle: Divide and Conquer Paradigm
date: 2019-07-05
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

- [Overview](#overview)
- [Divide and Conquer](#divide-and-conquer)
- [Early Historical Examples](#early-historical-examples)
- [Advantages](#advantages)
    - [Solving difficult problems](#solving-difficult-problems)
    - [Algorithm efficiency](#algorithm-efficiency)
    - [Parallelism](#parallelism)
    - [Memory access](#memory-access)
    - [Roundoff control](#roundoff-control)
- [Implementation Issues](#implementation-issues)
    - [Recursion](#recursion)
    - [Explicit Stack](#explicit-stack)
    - [Stack Size](#stack-size)
    - [Choosing the base cases](#choosing-the-base-cases)
    - [Sharing repeated subproblems](#sharing-repeated-subproblems)

## Overview
In Computer Science, Divide and Conquer is an algorithm design paradigm based on multi-branched recursion. A Divide-and-Conquer algorithm works by recursively breaking down a problem into two or more sub-problems of the same or related type, until these become simple enough to be solved directly. The solutions to the sub-problems are then combined to give a solution to the original problem.

This Divide-and-Conquer technique is the basis of efficient algorithms for all kinds of problems, such as `sorting` (e.g., <ins>quicksort</ins>, <ins>merge sort</ins>), `multiplying large numbers` (e.g. the <ins>Karatsuba algorithm</ins>), `finding the closest pair of points`, `syntactic analysis` (e.g., <ins>Top-down Parsers</ins>), and computing the `Discrete Fourier Transform` (DFT).

Understanding and designing Divide-and-Conquer algorithms is a complex skill that requires a good understanding of the nature of the underlying problem to be solved. As when proving a theorem by induction, it is often necessary to replace the original problem with a more general or complicated problem in order to initialize the recursion, and there is no systematic method for finding the proper generalization. These Divide-and-Conquer complications are seen when optimizing the calculation of a Fibonacci number with efficient double recursion.

The correctness of a Divide-and-Conquer algorithm is usually proved by Mathematical Induction, and its computational cost is often determined by solving recurrence relations.

## Divide and Conquer
The Divide-and-Conquer paradigm is often used to find an optimal solution of a problem. Its basic idea is to decompose a given problem into two or more similar, but simpler, subproblems, to solve them in turn, and to compose their solutions to solve the given problem. Problems of sufficient simplicity are solved directly. For example, to sort a given list of <strong>n</strong> natural numbers, split it into two lists of about <strong>n/2</strong> numbers each, sort each of them in turn, and interleave both results appropriately to obtain the sorted version of the given list. This approach is known as the `Merge Sort` algorithm.

![ZaUNT0.png](https://s2.ax1x.com/2019/07/05/ZaUNT0.png)
Divide-and-conquer approach to sort the list (38, 27, 43, 3, 9, 82, 10) in increasing order.
- Upper half: splitting into sublists;
- Mid: a one-element list is trivially sorted;
- Lower half: composing sorted sublists.

The name "Divide and Conquer" is sometimes applied to algorithms that reduce each problem to only one sub-problem, such as the `Binary Search` algorithm for finding a record in a sorted list (or its analog in `Numerical Computing`, the `Bisection Algorithm` for root finding). These algorithms can be implemented more efficiently than general divide-and-conquer algorithms; in particular, if they use tail recursion, they can be converted into simple loops. Under this broad definition, however, every algorithm that uses recursion or loops could be regarded as a "Divide-and-Conquer algorithm". Therefore, some authors consider that the name "Divide and Conquer" should be used only when each problem may generate two or more subproblems. The name `Decrease and Conquer` has been proposed instead for the single-subproblem class.

An important application of Divide and Conquer is in `Optimization`, where if the search space is reduced ("pruned") by a constant factor at each step, the overall algorithm has the same asymptotic complexity as the pruning step, with the constant depending on the pruning factor (by summing the geometric series); this is known as `Prune and Search`.

## Early Historical Examples
Early examples of these algorithms are primarily `Decrease and Conquer` – the original problem is successively broken down into single subproblems, and indeed can be solved iteratively.

`Binary Search`, a `Decrease-and-Conquer` algorithm where the subproblems are of roughly half the original size, has a long history. While a clear description of the algorithm on computers appeared in 1946 in an article by <strong>John Mauchly</strong>, the idea of using a sorted list of items to facilitate searching dates back at least as far as Babylonia in 200 BC. Another ancient `Decrease-and-Conquer` algorithm is the <strong>Euclidean Algorithm</strong> to compute the `Greatest Common Divisor` of two numbers by reducing the numbers to smaller and smaller equivalent subproblems, which dates to several centuries BC.

An early example of a Divide-and-Conquer Algorithm with multiple subproblems is <strong>Gauss</strong>'s 1805 description of what is now called the `Cooley–Tukey Fast Fourier Transform` (FFT) algorithm, although he did not analyze its operation count quantitatively, and FFTs did not become widespread until they were rediscovered over a century later.

An early two-subproblem Divide-and-Conquer Algorithm that was specifically developed for computers and properly analyzed is the `Merge Sort` algorithm, invented by <strong>John von Neumann</strong> in 1945.

Another notable example is the algorithm invented by <strong>Anatolii A. Karatsuba</strong> in 1960 that could multiply two n-digit numbers in ![ZarKDe.png](https://s2.ax1x.com/2019/07/05/ZarKDe.png) operations (in Big O notation). This algorithm disproved <strong>Andrey Kolmogorov</strong>'s 1956 conjecture that ![Zar34I.png](https://s2.ax1x.com/2019/07/05/Zar34I.png) operations would be required for that task.

As another example of a <strong>Divide-and-Conquer Algorithm</strong> that did not originally involve computers, <strong>Donald Knuth</strong> gives the method a post office typically uses to route mail: letters are sorted into separate bags for different geographical areas, each of these bags is itself sorted into batches for smaller sub-regions, and so on until they are delivered. This is related to a <strong>Radix Sort</strong>, described for <strong>Punch-Card Sorting</strong> machines as early as 1929.

## Advantages
#### Solving difficult problems
<strong>Divide and Conquer</strong> is a powerful tool for solving conceptually difficult problems: all it requires is a way of breaking the problem into sub-problems, of solving the trivial cases and of combining sub-problems to the original problem. Similarly, <strong>Decrease and Conquer</strong> only requires reducing the problem to a single smaller problem, such as the classic `Tower of Hanoi` puzzle, which reduces moving a tower of height <strong>n</strong> to moving a tower of height <strong>n − 1</strong>.

#### Algorithm efficiency
The <strong>Divide-and-Conquer</strong> paradigm often helps in the discovery of efficient algorithms. It was the key, for example, to `Karatsuba's Fast Multiplication Method`, the `Quicksort` and `Mergesort` Algorithms, the `Strassen Algorithm` for matrix multiplication, and `Fast Fourier Transforms`.

In all these examples, the <strong>Divide-and-Conquer</strong> approach led to an improvement in the <strong>Asymptotic Cost</strong> of the solution. For example, if
1. the base cases have constant-bounded size, the work of splitting the problem and combining the partial solutions is proportional to the problem's size <strong>n</strong>
2. there is a bounded number <strong>p</strong> of subproblems of size ~ <strong>n/p</strong> at each stage

then the cost of the <strong>Divide-and-Conquer Algorithm</strong> will be <strong>O(n logpn)</strong>.

#### Parallelism
<strong>Divide-and-Conquer Algorithms</strong> are naturally adapted for execution in multi-processor machines, especially shared-memory systems where the communication of data between processors does not need to be planned in advance, because distinct sub-problems can be executed on different processors.

#### Memory access
<strong>Divide-and-Conquer Algorithms</strong> naturally tend to make efficient use of memory caches. The reason is that once a sub-problem is small enough, it and all its sub-problems can, in principle, be solved within the cache, without accessing the slower main memory. An algorithm designed to exploit the cache in this way is called `Cache-Oblivious`, because it does not contain the cache size as an explicit parameter. Moreover, <strong>Divide-and-Conquer Algorithms</strong> can be designed for important algorithms (e.g., `Sorting`, `Fast Fourier Transforms`, and `Strassen Algorithm` for matrix multiplication) to be optimal Cache-Oblivious algorithms–they use the cache in a probably optimal way, in an asymptotic sense, regardless of the cache size. In contrast, the traditional approach to exploiting the cache is <strong>blocking</strong>, as in loop nest optimization, where the problem is explicitly divided into chunks of the appropriate size—this can also use the cache optimally, but only when the algorithm is tuned for the specific cache size(s) of a particular machine.

The same advantage exists with regards to other hierarchical storage systems, such as <strong>NUMA</strong> or <strong>Virtual Memory</strong>, as well as for multiple levels of cache: once a sub-problem is small enough, it can be solved within a given level of the hierarchy, without accessing the higher (slower) levels.

#### Roundoff control
In computations with rounded arithmetic, e.g. with floating-point numbers, a <strong>Divide-and-Conquer Algorithms</strong> may yield more accurate results than a superficially equivalent iterative method. For example, one can add <strong>N</strong> numbers either by a simple loop that adds each datum to a single variable, or by a <strong>Divide-and-Conquer Algorithms</strong> called `Pairwise Summation` that breaks the data set into two halves, recursively computes the sum of each half, and then adds the two sums. While the second method performs the same number of additions as the first, and pays the overhead of the recursive calls, it is usually more accurate

## Implementation Issues
#### Recursion
<strong>Divide-and-Conquer Algorithms</strong> are naturally implemented as recursive procedures. In that case, the partial sub-problems leading to the one currently being solved are automatically stored in the procedure call stack. A recursive function is a function that calls itself within its definition.

#### Explicit Stack
<strong>Divide-and-Conquer Algorithms</strong> can also be implemented by a non-recursive program that stores the partial sub-problems in some explicit data structure, such as a <strong>Stack</strong>, <strong>Queue</strong>, or <strong>Priority Queue</strong>. This approach allows more freedom in the choice of the sub-problem that is to be solved next, a feature that is important in some applications — e.g. in `Breadth-First Recursion` and the `Branch-and-Bound` method for function optimization. This approach is also the standard solution in programming languages that do not provide support for recursive procedures.

#### Stack Size
In recursive implementations of <strong>Divide-and-Conquer Algorithms</strong>, one must make sure that there is sufficient memory allocated for the recursion stack, otherwise the execution may fail because of stack overflow. <strong>Divide-and-Conquer Algorithms</strong> that are time-efficient often have relatively small recursion depth. For example, the quicksort algorithm can be implemented so that it never requires more than ![ZagdtH.png](https://s2.ax1x.com/2019/07/05/ZagdtH.png) nested recursive calls to sort <strong>n</strong> items.

<strong>Stack Overflow</strong> may be difficult to avoid when using recursive procedures, since many compilers assume that the recursion stack is a contiguous area of memory, and some allocate a fixed amount of space for it. Compilers may also save more information in the recursion stack than is strictly necessary, such as <strong>return address</strong>, <strong>unchanging parameters</strong>, and <strong>the internal variables of the procedure</strong>. Thus, the risk of <strong>Stack Overflow</strong> can be reduced by minimizing the parameters and internal variables of the recursive procedure or by using an explicit stack structure.

#### Choosing the base cases
In any recursive algorithm, there is considerable freedom in the choice of the base cases, the small subproblems that are solved directly in order to terminate the recursion.

Choosing the smallest or simplest possible base cases is more elegant and usually leads to simpler programs, because there are fewer cases to consider and they are easier to solve. For example, an FFT algorithm could stop the recursion when the input is a single sample, and the quicksort list-sorting algorithm could stop when the input is the empty list; in both examples there is only one base case to consider, and it requires no processing.

On the other hand, efficiency often improves if the recursion is stopped at relatively large base cases, and these are solved non-recursively, resulting in a hybrid algorithm. This strategy avoids the overhead of recursive calls that do little or no work, and may also allow the use of specialized non-recursive algorithms that, for those base cases, are more efficient than explicit recursion. A general procedure for a simple hybrid recursive algorithm is short-circuiting the base case, also known as `Arm's-Length Recursion`. In this case whether the next step will result in the base case is checked before the function call, avoiding an unnecessary function call. For example, in a tree, rather than recursing to a child node and then checking whether it is null, checking null before recursing; this avoids half the function calls in some algorithms on binary trees. Since a <strong>Divide-and-Conquer Algorithms</strong> eventually reduces each problem or sub-problem instance to a large number of base instances, these often dominate the overall cost of the algorithm, especially when the splitting/joining overhead is low. Note that these considerations do not depend on whether recursion is implemented by the compiler or by an explicit stack.

Thus, for example, many library implementations of quicksort will switch to a simple loop-based insertion sort (or similar) algorithm once the number of items to be sorted is sufficiently small. Note that, if the empty list were the only base case, sorting a list with n entries would entail maximally n quicksort calls that would do nothing but return immediately. Increasing the base cases to lists of size 2 or less will eliminate most of those do-nothing calls, and more generally a base case larger than 2 is typically used to reduce the fraction of time spent in function-call overhead or stack manipulation.

Alternatively, one can employ large base cases that still use a <strong>Divide-and-Conquer Algorithms</strong>, but implement the algorithm for predetermined set of fixed sizes where the algorithm can be completely unrolled into code that has no recursion, loops, or conditionals (related to the technique of partial evaluation). For example, this approach is used in some efficient FFT implementations, where the base cases are unrolled implementations of divide-and-conquer FFT algorithms for a set of fixed sizes. Source-code generation methods may be used to produce the large number of separate base cases desirable to implement this strategy efficiently.

The generalized version of this idea is known as recursion "unrolling" or "coarsening", and various techniques have been proposed for automating the procedure of enlarging the base case.

#### Sharing repeated subproblems
For some problems, the branched recursion may end up evaluating the same sub-problem many times over. In such cases it may be worth identifying and saving the solutions to these overlapping subproblems, a technique commonly known as `Memoization`. Followed to the limit, it leads to bottom-up <strong>Divide-and-Conquer Algorithms</strong> such as `Dynamic Programming` and `Chart Parsing`.
