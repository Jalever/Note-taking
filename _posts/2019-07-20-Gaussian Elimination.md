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

## Definitions and example of algorithm
The process of row reduction makes use of Elementary Row Operations, and can be divided into two parts. The first part (sometimes called <strong>Forward Elimination</strong>) reduces a given system to <strong>Row Echelon Form</strong>, from which one can tell whether there are no solutions, a unique solution, or infinitely many solutions. The second part (sometimes called <strong>Back Substitution</strong>) continues to use row operations until the solution is found; in other words, it puts the matrix into <strong>Reduced Row Echelon Form</strong>.

Another point of view, which turns out to be very useful to analyze the algorithm, is that row reduction produces a <strong>Matrix Decomposition</strong> of the original matrix. The elementary row operations may be viewed as the multiplication on the left of the original matrix by <strong>Elementary Matrices</strong>. Alternatively, a sequence of elementary operations that reduces a single row may be viewed as multiplication by a <strong>Frobenius Matrix</strong>. Then the first part of the algorithm computes an <strong>LU Decomposition</strong>, while the second part writes the original matrix as the product of a uniquely determined invertible matrix and a uniquely determined reduced row echelon matrix.

#### Row operations
There are three types of Elementary Row Operations which may be performed on the rows of a matrix:
1. Swap the positions of two rows.
2. Multiply a row by a non-zero scalar.
3. Add to one row a scalar multiple of another.

If the Matrix is associated to a system of Linear Equations, then these operations do not change the solution set. Therefore, if one's goal is to solve a system of Linear Equations, then using these row operations could make the problem easier.

#### Echelon form
For each row in a Matrix, if the row does not consist of only zeros, then the leftmost nonzero entry is called the <strong>Leading Coefficient</strong>(or <strong>Pivot</strong>) of that row. So if two Leading Coefficients are in the same column, then a row operation of <ins>Type 3</ins> could be used to make one of those coefficients zero. Then by using the row swapping operation, one can always order the rows so that for every non-zero row, the Leading Coefficient is to the right of the Leading Coefficient of the row above. If this is the case, then matrix is said to be in <strong>Row Echelon Form</strong>. So the lower left part of the Matrix contains only zeros, and all of the zero rows are below the non-zero rows. The word "echelon" is used here because one can roughly think of the rows being ranked by their size, with the largest being at the top and the smallest being at the bottom.

For example, the following Matrix is in Row Echelon Form, and its Leading Coefficients are shown in red:
![Zzz4gg.png](https://s2.ax1x.com/2019/07/20/Zzz4gg.png)
It is in Echelon Form because the zero row is at the bottom, and the Leading Coefficient of the second row (in the third column), is to the right of the Leading Coefficient of the first row (in the second column).

A matrix is said to be in <strong>Reduced Row Echelon Form</strong> if furthermore all of the Leading Coefficients are equal to 1 (which can be achieved by using the Elementary Row Operation of <ins>Type 2</ins>), and in every column containing a Leading Coefficient, all of the other entries in that column are zero (which can be achieved by using Elementary Row Operations of <ins>Type 3</ins>).
