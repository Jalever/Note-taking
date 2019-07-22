---
layout: post
title: Introduction to Permutation
subtitle: Combinatorics
date: 2019-07-21
author: Jalever
header-img: img/math_bg_simple.png
catalog: true
tags:
  - Mathematics
---

- [Overview](#overview)

## Overview
In Mathematics, <strong>Permutation</strong> is the act of arranging the members of a <ins>Set</ins> into a <ins>sequence</ins> or <ins>order</ins>, or, if the set is already ordered, rearranging (reordering) its elements—a process called <strong>Permuting</strong>. <strong>Permutation</strong>s differ from <strong>Combination</strong>s, which are selections of some members of a set regardless of order. For example, written as <strong>Tuples</strong>, there are six permutations of the set `{1,2,3}`, namely: `(1,2,3)`, `(1,3,2)`, `(2,1,3)`, `(2,3,1)`, `(3,1,2)`, and `(3,2,1)`. These are all the possible orderings of this three-element set. Anagrams of words whose letters are different are also permutations: the letters are already ordered in the original word, and the anagram is a reordering of the letters. The study of permutations of finite sets is an important topic in the fields of <strong>Combinatorics</strong> and <strong>Group Theory</strong>.

<strong>Permutations</strong> are studied in almost every branch of Mathematics, and in many other fields of science. In <strong>Computer Science</strong>, they are used for analyzing Sorting Algorithms; in <strong>Quantum Physics</strong>, for describing states of particles; and in <strong>Biology</strong>, for describing `RNA` sequences.

The number of permutations of `n` distinct objects is `n` factorial, usually written as `n!`, which means the product of all positive integers less than or equal to `n`.

In Algebra, and particularly in Group Theory, a permutation of a set `S` is defined as a Bijection from `S` to itself. That is, it is a function from `S` to `S` for which every element occurs exactly once as an <strong>Image</strong> value. This is related to the rearrangement of the elements of `S` in which each element `s` is replaced by the corresponding `f(s)`. For example, the permutation `(3,1,2)` mentioned above is described by the function &alpha; defined as:
![eSjZZt.png](https://s2.ax1x.com/2019/07/21/eSjZZt.png)

The collection of such permutations form a Group called the <strong>Symmetric Group of S</strong>. The key to this group's structure is the fact that the composition of two permutations (performing two given rearrangements in succession) results in another rearrangement. Permutations may act on structured objects by rearranging their components, or by certain replacements (substitutions) of symbols. Frequently the set used is ![eSjUiT.png](https://s2.ax1x.com/2019/07/21/eSjUiT.png), but there is no restriction on the set.

In Elementary Combinatorics, the <strong>K-Permutations</strong>, or <strong>Partial Permutations</strong>, are the ordered arrangements of `k` distinct elements selected from a set. When k is equal to the size of the set, these are the permutations of the set.
