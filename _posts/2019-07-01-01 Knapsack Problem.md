---
layout: post
title: 0-1 Knapsack Problem
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
    - [Source Codes Details](#source-codes-details)
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
![ZGGekn.png](https://s2.ax1x.com/2019/07/02/ZGGekn.png)

Let's try to understand on with this example. So here I have a two dimensional matrix and this is a my total number of columns is same as total weight plus one and my number of rows is same as the total items. So our first column is 0, It means that if the total weight is zero no matter what items I have my maximum value I can get is always zero. So this is why this all are zero.

![ZGGKpV.png](https://s2.ax1x.com/2019/07/02/ZGGKpV.png)

If I just had one item 1, the best I can do is 1. So this is the weight of item, the total weight is one. so the maximum value I can get is just 1.
![ZGG0XD.png](https://s2.ax1x.com/2019/07/02/ZGG0XD.png)


If my total weight is two, if I just had one item of weight 1 and whose value is 1 the best I can do is 1. Remember we just have one quantity of each item. So even though the total weight is 2 if I just have item 1 again the best I can do is value 1.
![ZGGo7j.png](https://s2.ax1x.com/2019/07/02/ZGGo7j.png)

Similarly, one, one, one, one, one. So if the total weight is 7 the only item I have is weight 1 and whose value is 1 the best I can do is one because we have one quantity of each item.
![ZGGjjU.png](https://s2.ax1x.com/2019/07/02/ZGGjjU.png)

So next let's introduce 3. Since the total weight is 1 and if the weight of the item is 3 which is greater than one so three can never be the, can never be selected. So what we do is what is the best we can do without selecting 3 so basically this number becomes one.
![ZGJEjO.png](https://s2.ax1x.com/2019/07/02/ZGJEjO.png)

Again 2, Since 2 is less than 3, 3 can never be selected. Since this total weight is less than 3 so the best we can do is without 3 what is the best we can do which is this number, so that's 1.
![ZGJJKS.png](https://s2.ax1x.com/2019/07/02/ZGJJKS.png)

Now 3,so since 3 is,since 3 is less equal to 3, we have 2 choices, do we select 3 or do we not select 3. If we select this item(weight is 3, value is 4) the so we have to check what is the best we can do by selecting this item. If we didn't select this item this gives me a value 4 plus whatever weight is remaining after we select this weight. So 3-3 so that's 0. So weight[0][0](the first 0 is to go back to previous row, and second one is because 3 minus 3 is equal to 0) and then and then we go to the top column so that's also 0(matrix[0][0] is 0). So we reach this point,so we up,we go 3 steps, we reach this point,3 steps because the weight of this item is 3 So T[0][0] is 0 or what is the best value we can do without selecting this item altogether and that's 1. So this value is 4 and this value is 1 so max of this is 4.
![ZGw9s0.png](https://s2.ax1x.com/2019/07/02/ZGw9s0.png)

so the total weight is 4 and the item weight is 3. So again the best I can do is without selecting 3 the best I'm getting is 1[row is (1)1, column is 1, which number is 1]. If I do select 3 the best I can get is max of by selecting 3 I get a value of 4 plus I subtract 3 from 4 so that's,that's 1. and then I go one row up which is 0 and 1. So this value 0 and 1 is 1, so 4 plus 1, 5 so max of 4 plus 1,5 or this value 1, so that's 5.
![ZGwoY4.png](https://s2.ax1x.com/2019/07/02/ZGwoY4.png)

...

![ZG0Ste.png](https://s2.ax1x.com/2019/07/02/ZG0Ste.png)

#### Source Codes Details
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

int getMaximum(int a, int b) {
  return (a > b)? a : b;
}

int Knapsack(int capacityOfKnapsack, int weight[], int value[], int numberOfItems) {

	int Matrix[numberOfItems + 1][capacityOfKnapsack + 1];

	for(int item=0;item <= numberOfItems;++item) {
		for(int column = 0;column <= capacityOfKnapsack;++column) {
			if(item == 0 || column == 0) {
				Matrix[item][column] = 0;
			} else if(column >= weight[item-1]) {
				Matrix[item][column] = getMaximum(value[item-1] + Matrix[item-1][column-weight[item-1]], Matrix[item-1][column]);
			} else {
				Matrix[item][column] = Matrix[item-1][column];
			}
		}
	}

	return Matrix[numberOfItems][capacityOfKnapsack];
}

int main() {
	int value[] = {1, 4, 5, 7};
	int weight[] = {1, 3, 4, 5};
	int W = 7;
	int n = sizeof(value)/sizeof(value[0]);
	cout << "Maximum value is " << Knapsack(W, weight, value, n) << endl;
	return 0;
}


```

#### Time Complexity
Time Complexity: `O(nW)` where `n` is the number of items and `W` is the capacity of knapsack.
