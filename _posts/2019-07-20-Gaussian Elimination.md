---
layout: post
title: Gaussian Elimination
subtitle: Linear Algebra
date: 2019-07-20
author: Jalever
header-img: img/math_bg_simple.png
catalog: true
tags:
  - Mathematics
---

## Overview
<strong>Gaussian Elimination</strong>, also known as <strong>Row Reduction</strong>, is an algorithm in <strong>Linear Algebra</strong> for solving a <strong>System of Linear Equations</strong>. It is usually understood as a sequence of operations performed on the corresponding Matrix of coefficients. This method can also be used to find the <strong>Rank</strong> of a matrix, to calculate the <strong>Determinant</strong> of a matrix, and to calculate the inverse of an <strong>Invertible Square Matrix</strong>. The method is named after <i>Carl Friedrich Gauss</i>(1777–1855)

To perform <strong>Row Reduction</strong> on a Matrix, one uses a sequence of <strong>Elementary Row Operations</strong> to modify the matrix until the lower left-hand corner of the Matrix is filled with zeros, as much as possible. There are three types of elementary row operations:
- Swapping two rows,
- Multiplying a row by a nonzero number,
- Adding a multiple of one row to another row.

Using these operations, a Matrix can always be transformed into an <strong>Upper Triangular Matrix</strong>, and in fact one that is in <strong>Row Echelon Form</strong>. Once all of the <strong>Leading Coefficients</strong>(the leftmost nonzero entry in each row) are 1, and every column containing a <strong>Leading Coefficient</strong> has zeros elsewhere, the Matrix is said to be in <strong>Reduced Row Echelon Form</strong>. This final form is unique; in other words, it is independent of the sequence of row operations used. For example, in the following sequence of row operations (where multiple elementary operations might be done at each step), the third and fourth matrices are the ones in Row Echelon Form, and the final matrix is the unique Reduced Row Echelon Form.
![ZzjvgH.png](https://s2.ax1x.com/2019/07/20/ZzjvgH.png)

Using row operations to convert a Matrix into <strong>Reduced Row Echelon Form</strong> is sometimes called <strong>Gauss–Jordan Elimination</strong>. Some authors use the term <strong>Gaussian Elimination</strong> to refer to the process until it has reached its Upper Triangular, or (unreduced)Row Echelon Form. For computational reasons, when solving systems of Linear Equations, it is sometimes preferable to stop row operations before the Matrix is completely reduced.
