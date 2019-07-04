---
layout: post
title: Fractional Knapsack Problem
subtitle: Greedy Algorithm学习笔记系列
date: 2019-07-04
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

- [Introduction](#introduction)
- [Implementation in CPP](#implementation-in-cpp)
    - [Explanation of Codes](#explanation-of-codes)
    - [Sample Code](#sample-code)
    - [Time Complexity](#time-complexity)

## Introduction
Given weights and values of `n` items, we need to put these items in a knapsack of capacity `W` to get the maximum total value in the knapsack.

In Fractional Knapsack, we can break items for maximizing the total value of knapsack. This problem in which we can break an item is also called the `Fractional Knapsack Problem`.

```
Input :
    Items as (value, weight) pairs
    arr[] = {{60, 10}, {100, 20}, {120, 30}}
    Knapsack Capacity, W = 50;
Output :
   Maximum possible value = 240
   By taking full items of 10 kg, 20 kg and
   2/3rd of last item of 30 kg
```

A `Brute-Force` solution would be to try all possible subset with all different fraction but that will be too much time taking.

An efficient solution is to use `Greedy Approach`. The basic idea of the greedy approach is to calculate the ratio <ins>value</ins>/<ins>weight</ins> for each item and sort the item on basis of this ratio. Then take the item with the highest ratio and add them until we can’t add the next item as a whole and at the end add the next item as much as we can. Which will always be the optimal solution to this problem.

## Implementation in CPP
#### Explanation of Codes
constructor initialization lists, which is a method of initializing member variables using a constructor, consist of a colon after the constructor name, and then a comma-separated list of "function-like" statements which can be used to set member variables.

Parameters or constant values can be specified inside brackets next to the name of the member variable which you want to set
```cpp
struct Item{
	int value,weight;

    // value = v, weight = w

	Item(int v,int w) : value(v) , weight(w) {};
};
```

`sort(first, last, compare function)`, [first,last) contains all the elements between first and last, including the element pointed by first but not the element pointed by last.
```cpp
sort(arr, arr+length, getMaximum);
```

#### Sample Code
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Item{
	int value,weight;

	Item(int v,int w) : value(v) , weight(w) {};
};

bool getMaximum(struct Item a,struct Item b) {
	double r1 = (double)a.value/a.weight;
	double r2 = (double)b.value/b.weight;

	return r1 > r2;
};

double FractionalKnapsack(int capacityOfKnapsack,struct Item arr[],int length) {

	sort(arr, arr+length, getMaximum);

	int WeightSum = 0;
	double ValueSum = 0.0;

	for(int i = 0;i < length;i++) {
		if(WeightSum + arr[i].weight <= capacityOfKnapsack) {
			WeightSum += arr[i].weight;
			ValueSum += arr[i].value;
		} else {
			int remaining = capacityOfKnapsack - WeightSum;

			ValueSum += arr[i].value * ((double)remaining / arr[i].weight);
		}
	}

	return ValueSum;
};

int main() {
	int capacityOfKnapsack = 50;
	Item arr[] = {
			{60, 10},
			{100, 20},
			{120, 30}
	};

	int length = sizeof(arr)/sizeof(arr[0]);

	cout << "Maximum Value We can Obtain: " << endl;
	cout << ::FractionalKnapsack(capacityOfKnapsack, arr, length);

	return 0;
}

```

#### Time Complexity
As main time taking step is sorting, the whole problem can be solved in `O(n log n)` only.
