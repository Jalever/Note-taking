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

The coefficient `a` in the term of `a * x^b * y^c` is known as the <strong>Binomial Coefficient</strong> ![ZOhf9e.png](https://s2.ax1x.com/2019/07/18/ZOhf9e.png) or {\displaystyle {\tbinom {n}{c}}} {\tbinom {n}{c}} (the two have the same value). These coefficients for varying `n` and `b` can be arranged to form <strong>Pascal's Triangle</strong>. These numbers also arise in <strong>Combinatorics</strong>, where ![ZOhf9e.png](https://s2.ax1x.com/2019/07/18/ZOhf9e.png) gives the number of different combinations of `b` elements that can be chosen from an n-element set. Therefore ![ZOhf9e.png](https://s2.ax1x.com/2019/07/18/ZOhf9e.png) is often pronounced as "n choose b".
