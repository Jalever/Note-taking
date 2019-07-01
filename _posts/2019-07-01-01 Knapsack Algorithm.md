---
layout: post
title: 0-1 Knapsack Algorithm
subtitle: Dynamic Programming学习笔记系列
date: 2019-07-01
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

- [Overview](#overview)
    - [Optimal Substructure](#optimal-substructure)
    - [Overlapping Subproblems](#overlapping-subproblems)
- [Dynamic Programming Based Implementation](#dynamic-programming-based-implementation)
    - [Explanation](#explanation)
    - [Source Codes](#source-codes)

## Overview
Given weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack.

In other words, given two integer arrays `val[0..n-1]` and `wt[0..n-1]` which represent <ins>values</ins> and <ins>weights</ins> associated with `n items` respectively. Also given an integer `W` which represents <ins>knapsack capacity</ins>, find out the maximum value subset of `val[]` such that sum of the weights of this subset is smaller than or equal to `W`.

You cannot break an item, either pick the complete item, or don’t pick it (0-1 property).

A simple solution is to consider all subsets of items and calculate the total weight and value of all subsets. Consider the only subsets whose total weight is smaller than `W`. From all such subsets, pick the maximum value subset.

#### Optimal Substructure
To consider all subsets of items, there can be two cases for every item:
1. the item is included in the optimal subset
2. not included in the optimal set.

Therefore, the maximum value that can be obtained from n items is max of following two values.
1. Maximum value obtained by n-1 items and W weight (excluding nth item).
2. Value of nth item plus maximum value obtained by n-1 items and W minus weight of the nth item (including nth item).

If weight of nth item is greater than `W`, then the nth item cannot be included and <ins>case 1</ins> is the only possibility.

#### Overlapping Subproblems

## Dynamic Programming Based Implementation

#### Explanation

When `i = 0`
```text
   0   1   2   3
0  0   0   0   0
1  0
2  0
3  0
4  0
...
50 0
```

When `i = 1`
![Z8HrdS.png](https://s2.ax1x.com/2019/07/01/Z8HrdS.png)

![Z8HsIg.png](https://s2.ax1x.com/2019/07/01/Z8HsIg.png)

When `i = 2`
![Z8HcGj.png](https://s2.ax1x.com/2019/07/01/Z8HcGj.png)

![Z8HgRs.png](https://s2.ax1x.com/2019/07/01/Z8HgRs.png)

When `i = 3`
![Z8HWMq.png](https://s2.ax1x.com/2019/07/01/Z8HWMq.png)

![Z8Hfs0.png](https://s2.ax1x.com/2019/07/01/Z8Hfs0.png)

#### Source Codes
```cpp
#include<iostream>
using namespace std;

// A utility function that returns maximum of two integers
int max(int a, int b) {
  return (a > b)? a : b;
}

// Returns the maximum value that can be put in a knapsack of capacity W
int knapSack(int capacityOfKnapsack, int weight[], int val[], int numberOfItems) {
	int i, w;
	int temporaryArray[numberOfItems+1][capacityOfKnapsack+1];

	for (i = 0; i <= numberOfItems; i++) {
		for (w = 0; w <= capacityOfKnapsack; w++) {
			if (i==0 || w==0) {
				temporaryArray[i][w] = 0;
			} else if (weight[i-1] <= w) {

				temporaryArray[i][w] = max(val[i-1] + temporaryArray[i-1][w-weight[i-1]], temporaryArray[i-1][w]);

			} else {
				temporaryArray[i][w] = temporaryArray[i-1][w];
			}
		}
	}

	return temporaryArray[numberOfItems][capacityOfKnapsack];
}

int main() {
	int value[] = {60, 100, 120};
	int weight[] = {10, 20, 30};
	int W = 50;
	int n = sizeof(value)/sizeof(value[0]);
	cout << "Maximum value is " << knapSack(W, weight, value, n) << endl;
	return 0;
}

```
