---
layout: post
title: Binomial Coefficient
subtitle: Dynamic Programming Paradigm
date: 2019-07-01
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
- [Common Definition](#common-definition)
    - [Coefficient](#coefficient)
    - [Binomial Theorem](#binomial-theorem)
    - [Binomial Coefficient](#binomial-coefficient)
    - [Pascal Triangle](#pascal-triangle)

## Common Definition
#### Coefficient
In <strong>Mathematics</strong>, a <strong>Coefficient</strong> is a multiplicative factor in some term of a <ins>polynomial</ins>, a <ins>series</ins>, or <ins>any expression</ins>; it is usually a <ins>number</ins>, but may be <ins>any expression</ins>. In the latter case, the variables appearing in the coefficients are often called <strong>Parameter</strong>s, and must be clearly distinguished from the other variables.

For example, in
![ZOspFA.png](https://s2.ax1x.com/2019/07/18/ZOspFA.png)
the first two terms respectively have the coefficients `7` and `−3`. The third term `1.5` is a constant coefficient. The final term does not have any explicitly written coefficient, but is considered to have coefficient `1`, since multiplying by that factor would not change the term.

Often <strong>Coefficient</strong>s are numbers as in this example, although they could be <strong>parameter</strong>s of the problem or <strong>any expression</strong> in these parameters. In such a case one must clearly distinguish between <ins>symbols representing variables</ins> and <ins>symbols representing parameters</ins>. Following <strong>René Descartes</strong>, the <strong>variables</strong> are often denoted by `x, y, ...`, and the <strong>parameter</strong>s by `a, b, c, ...`, but it is not always the case. For example, if `y` is considered as a parameter in the above expression, the coefficient of `x` is `−3y`, and the constant coefficient is `1.5 + y`.

When one writes
![ZOsllV.png](https://s2.ax1x.com/2019/07/18/ZOsllV.png)
it is generally supposed that `x` is the only variable and that `a`, `b` and `c` are parameters; thus the constant coefficient is `c` in this case.

#### Binomial Theorem
In <strong>Elementary Algebra</strong>, the <strong>Binomial Theorem</strong>(or <strong>Binomial Expansion</strong>) describes the algebraic expansion of powers of a binomial. According to the theorem, it is possible to expand the polynomial `(x + y)^n` into a sum involving terms of the form `a * x^b * y^c`, where the exponents `b` and `c` are nonnegative integers with `b + c = n`, and the coefficient `a` of each term is a specific positive integer depending on `n` and `b`. For example (for n = 4),
![ZO2roF.png](https://s2.ax1x.com/2019/07/18/ZO2roF.png)

The coefficient `a` in the term of `a * x^b * y^c` is known as the <strong>Binomial Coefficient</strong> ![ZOhf9e.png](https://s2.ax1x.com/2019/07/18/ZOhf9e.png) or ![ZO4nD1.png](https://s2.ax1x.com/2019/07/18/ZO4nD1.png) (the two have the same value). These coefficients for varying `n` and `b` can be arranged to form <strong>Pascal's Triangle</strong>. These numbers also arise in <strong>Combinatorics</strong>, where ![ZOhf9e.png](https://s2.ax1x.com/2019/07/18/ZOhf9e.png) gives the number of different combinations of `b` elements that can be chosen from an n-element set. Therefore ![ZOhf9e.png](https://s2.ax1x.com/2019/07/18/ZOhf9e.png) is often pronounced as "n choose b".

#### Binomial Coefficient
In <strong>Mathematics</strong>, the <strong>Binomial Coefficients</strong> are the positive integers that occur as coefficients in the <strong>Binomial Theorem</strong>. Commonly, a <strong>Binomial Coefficient</strong> is indexed by a pair of integers `n >= k >= 0` and is written ![ZO5CMd.png](https://s2.ax1x.com/2019/07/18/ZO5CMd.png). It is the coefficient of the `x^k` term in the <strong>Polynomial Expansion</strong> of the <strong>Binomial Power</strong> `(1 + x)^n`, and it is given by the formula
![ZO5KMj.png](https://s2.ax1x.com/2019/07/18/ZO5KMj.png)

For example, the fourth power of `1 + x` is
![ZO53d0.png](https://s2.ax1x.com/2019/07/18/ZO53d0.png)
and the binomial coefficient![ZO5JiT.png](https://s2.ax1x.com/2019/07/18/ZO5JiT.png)is the coefficient of the `x^2` term.

Arranging the numbers ![ZOIeTx.png](https://s2.ax1x.com/2019/07/18/ZOIeTx.png)in successive rows for `n = 0, 1, 2,...` gives a triangular array called <strong>Pascal's Triangle</strong>, satisfying the <strong>Recurrence Relation</strong>.
![ZOIw9S.png](https://s2.ax1x.com/2019/07/18/ZOIw9S.png)

The binomial coefficients occur in many areas of mathematics, and especially in combinatorics. The symbol ![ZO5CMd.png](https://s2.ax1x.com/2019/07/18/ZO5CMd.png) is usually read as "n choose k" because there are ![ZO5CMd.png](https://s2.ax1x.com/2019/07/18/ZO5CMd.png) ways to choose an (unordered) subset of `k` elements from a fixed set of `n` elements. For example, there are ![ZOI5jJ.png](https://s2.ax1x.com/2019/07/18/ZOI5jJ.png) ways to choose 2 elements from `{1, 2, 3, 4}`, namely `{1, 2}`, `{1, 3}`, `{1, 4}`, `{2, 3}`, `{2, 4}` and  `{3, 4}`.

#### Pascal Triangle
In <strong>Mathematics</strong>, <strong>Pascal's Triangle</strong> is a triangular array of the <strong>Binomial Coefficient</strong>s.

In <strong>Pascal's Triangle</strong>, each number is the sum of the two numbers directly above it.

![ZO56JO.gif](https://s2.ax1x.com/2019/07/18/ZO56JO.gif)
For example, the fourth power of `1 + x` is
![ZO53d0.png](https://s2.ax1x.com/2019/07/18/ZO53d0.png)
