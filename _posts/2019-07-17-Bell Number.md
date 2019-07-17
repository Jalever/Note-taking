---
layout: post
title: Bell Number
subtitle: Dynamic Programming Paradigm
date: 2019-07-01
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
## Overview
Given a set of n elements, find number of ways of partitioning it.

Examples:
![Zq2u2q.png](https://s2.ax1x.com/2019/07/17/Zq2u2q.png)
Solution to above questions is <strong>Bell Number</strong>.

In <strong>Combinatorial Mathematics</strong>, the <strong>Bell Numbers</strong> count the possible Partitions of a Set. These numbers have been studied by mathematicians since the 19th century, and their roots go back to medieval Japan, but they are named after <strong>Eric Temple Bell</strong>, who wrote about them in the 1930s.

Starting with `B0 = B1 = 1`, the first few Bell numbers are:

`1, 1, 2, 5, 15, 52, 203, 877, 4140, 21147, 115975, 678570, 4213597, 27644437, 190899322, 1382958545, 10480142147, 82864869804, 682076806159, 5832742205057, ...`

The `nth` of these numbers, `Bn`, counts the number of different ways to partition a set that has exactly `n` elements, or equivalently, the number of equivalence relations on it. Outside of mathematics, the same number also counts the number of different Rhyme Schemes for n-line poems.

As well as appearing in counting problems, these numbers have a different interpretation, as moments of Probability Distributions. In particular, `Bn` is the nth moment of a Poisson Distribution with mean 1.

In general, `Bn` is the number of partitions of a set of size n. A partition of a set S is defined as a set of nonempty, pairwise disjoint subsets of S whose union is S. For example, `B3 = 5` because the 3-element set `{a, b, c}` can be partitioned in 5 distinct ways:
![ZqRzct.png](https://s2.ax1x.com/2019/07/17/ZqRzct.png)

`B0` is 1 because there is exactly one partition of the empty set. Every member of the empty set is a nonempty set (that is vacuously true), and their union is the empty set. Therefore, the empty set is the only partition of itself. As suggested by the set notation above, we consider neither <ins>the order of the partitions</ins> nor <ins>the order of elements within each partition</ins>. This means that the following partitionings are all considered identical:
![ZqWPHS.png](https://s2.ax1x.com/2019/07/17/ZqWPHS.png)

If, instead, different orderings of the sets are considered to be different partitions, then the number of these ordered partitions is given by the <strong>Ordered Bell Numbers</strong>.

## Triangle Scheme for calculations
The <strong>Bell Numbers</strong> can easily be calculated by creating the so-called <strong>Bell Triangle</strong>, also called <strong>Aitken's Array</strong> or the <strong>Peirce Triangle</strong> after <strong>Alexander Aitken</strong> and <strong>Charles Sanders Peirce</strong>.

1. Start with the number one. Put this on a row by itself.
2. Start a new row with the rightmost element from the previous row as the leftmost number
3. Determine the numbers not on the left column by taking the sum of the number to the left and the number above the number to the left, that is, the number diagonally up and left of the number we are calculating
4. Repeat step three until there is a new row with one more number than the previous row
5. The number on the left hand side of a given row is the Bell number for that row.

Here are the first five rows of the triangle constructed by these rules:
![ZqWYg1.png](https://s2.ax1x.com/2019/07/17/ZqWYg1.png)

The Bell numbers appear on both the left and right sides of the triangle.

## Implementation in CPP
```js
#include <iostream>
using namespace std;

int Bell(int n) {
	int arr[n+1][n+1];
	arr[0][0] = 1;

	for(int i=1;i <= n;i++) {
		arr[i][0] = arr[i-1][i-1];

		for(int j=1;j <= i;j++) {
			arr[i][j] = arr[i-1][j-1] + arr[i][j-1];
		}
	}

	return arr[n][0];
}

int main() {
	int value;
	cout << "Please input a value: ";
	cin >> value;

	for(int i = 0;i <= value;i++ ) {
		cout << "Bell Number[" << i << "] is " << ::Bell(i) << endl;
	}

	return 0;
}
```
