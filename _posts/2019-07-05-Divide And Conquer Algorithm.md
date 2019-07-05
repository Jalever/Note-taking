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

## Overview
In Computer Science, Divide and Conquer is an algorithm design paradigm based on multi-branched recursion. A Divide-and-Conquer algorithm works by recursively breaking down a problem into two or more sub-problems of the same or related type, until these become simple enough to be solved directly. The solutions to the sub-problems are then combined to give a solution to the original problem.

This Divide-and-Conquer technique is the basis of efficient algorithms for all kinds of problems, such as `sorting` (e.g., <ins>quicksort</ins>, <ins>merge sort</ins>), `multiplying large numbers` (e.g. the <ins>Karatsuba algorithm</ins>), `finding the closest pair of points`, `syntactic analysis` (e.g., <ins>Top-down Parsers</ins>), and computing the `Discrete Fourier Transform` (DFT).

Understanding and designing Divide-and-Conquer algorithms is a complex skill that requires a good understanding of the nature of the underlying problem to be solved. As when proving a theorem by induction, it is often necessary to replace the original problem with a more general or complicated problem in order to initialize the recursion, and there is no systematic method for finding the proper generalization. These Divide-and-Conquer complications are seen when optimizing the calculation of a Fibonacci number with efficient double recursion.

The correctness of a Divide-and-Conquer algorithm is usually proved by Mathematical Induction, and its computational cost is often determined by solving recurrence relations.

## Divide and Conquer
The Divide-and-Conquer paradigm is often used to find an optimal solution of a problem. Its basic idea is to decompose a given problem into two or more similar, but simpler, subproblems, to solve them in turn, and to compose their solutions to solve the given problem. Problems of sufficient simplicity are solved directly. For example, to sort a given list of `n` natural numbers, split it into two lists of about `n/2` numbers each, sort each of them in turn, and interleave both results appropriately to obtain the sorted version of the given list. This approach is known as the `Merge Sort` algorithm.

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

Another notable example is the algorithm invented by <strong>Anatolii A. Karatsuba</strong> in 1960 that could multiply two n-digit numbers in <img src="https://s2.ax1x.com/2019/07/05/ZarKDe.png" alt="ZarKDe.png" border="0" /> operations (in Big O notation). This algorithm disproved <strong>Andrey Kolmogorov</strong>'s 1956 conjecture that <img src="https://s2.ax1x.com/2019/07/05/Zar34I.png" alt="Zar34I.png" border="0" /> operations would be required for that task.

As another example of a <strong>Divide-and-Conquer Algorithm</strong> that did not originally involve computers, <strong>Donald Knuth</strong> gives the method a post office typically uses to route mail: letters are sorted into separate bags for different geographical areas, each of these bags is itself sorted into batches for smaller sub-regions, and so on until they are delivered. This is related to a <strong>Radix Sort</strong>, described for <strong>Punch-Card Sorting</strong> machines as early as 1929.
