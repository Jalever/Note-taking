---
layout: post
title: Introduction to Combination
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
In Mathematics, a <strong>Combination</strong> is a selection of items from a collection, such that (unlike Permutations) the order of selection does not matter. For example, given three fruits, say an apple, an orange and a pear, there are three combinations of two that can be drawn from this set: an apple and a pear; an apple and an orange; or a pear and an orange. More formally, a k-combination of a set `S` is a subset of `k` distinct elements of `S`. If the set has `n` elements, the number of k-combinations is equal to the Binomial Coefficient
![eFQOhR.png](https://s2.ax1x.com/2019/07/23/eFQOhR.png)
which can be written using factorials as ![eFlCHe.png](https://s2.ax1x.com/2019/07/23/eFlCHe.png) whenever `k <= n`, and which is zero when `k > n`. The set of all k-combinations of a set `S` is often denoted by ![eFlE9I.png](https://s2.ax1x.com/2019/07/23/eFlE9I.png).

Combinations refer to the combination of `n` things taken `k` at a time without repetition. To refer to combinations in which repetition is allowed, the terms <strong>k-selection</strong>, <strong>k-multiset</strong>, or <strong>k-combination</strong> with repetition are often used. If, in the above example, it were possible to have two of any one kind of fruit there would be 3 more 2-selections: one with two apples, one with two oranges, and one with two pears.

Although the set of three fruits was small enough to write a complete list of combinations, with large sets this becomes impractical. For example, a Poker Hand can be described as a 5-combination(k = 5) of cards from a 52 card deck(n = 52). The 5 cards of the hand are all distinct, and the order of cards in the hand does not matter. There are `2,598,960` such combinations, and the chance of drawing any one hand at random is `1 / 2,598,960`.
