---
layout: post
title: Maximum Subarray Sum using Divide and Conquer Algorithm
subtitle: Divide and Conquer Paradigm
date: 2019-07-05
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
- [Introduction](#introduction)
- [Solutions](#solutions)
    - [Naive Algorithm](#naive-algorithm)
    - [Divide And Conquer Algorithm](#divide-and-conquer-algorithm)
- [Implementation using Divide and Conquer Algorithm in CPP](#implementation-using-divide-and-conquer-algorithm-in-cpp)
    - [Time Complexity](#time-complexity)
- [Comparison with Kadane Algorithm](#comparison-with-kadane-algorithm)

## Introduction
You are given a one dimensional array that may contain both positive and negative integers, find the sum of contiguous subarray of numbers which has the largest sum.
For example, if the given array is `{-2, -5, 6, -2, -3, 1, 5, -6}`, then the maximum subarray sum is `7`

## Solutions

#### Naive Algorithm
The naive method is to run two loops. The outer loop picks the beginning element, the inner loop finds the maximum possible sum with first element picked by outer loop and compares this maximum with the overall maximum. Finally return the overall maximum. The time complexity of the Naive method is `O(n^2)`.

#### Divide And Conquer Algorithm
Using Divide and Conquer approach, we can find the maximum subarray sum in `O(nLogn)` time. Following is the Divide and Conquer algorithm.
1. Divide the given array in two halves
2. Return the maximum of following three
    2.1 Maximum subarray sum in left half (Make a recursive call)
    2.2 Maximum subarray sum in right half (Make a recursive call)
    2.3 Maximum subarray sum such that the subarray crosses the midpoint

The lines 2.a and 2.b are simple recursive calls.

How to find maximum subarray sum such that the subarray crosses the midpoint? We can easily find the crossing sum in linear time. The idea is simple, find the maximum sum starting from mid point and ending at some point on left of mid, then find the maximum sum starting from mid + 1 and ending with sum point on right of mid + 1. Finally, combine the two and return.

## Implementation using Divide and Conquer Algorithm in CPP
```cpp
#include <bits/stdc++.h>
#include <limits.h>
using namespace std;

int getMaximumOfTwo(int a,int b) {
	return (a>b) ? a : b;
}

int getMaximumOfThree(int a,int b,int c) {
	return ::getMaximumOfTwo(a, ::getMaximumOfTwo(b, c));
}

int getMaximumCrossingSum(int arr[],int firstIndex,int middleIndex,int lastIndex) {

	int temporarySum = 0;
	int leftSum = INT_MIN;
	for(int i = middleIndex;i >= firstIndex;--i) {
		temporarySum = temporarySum + arr[i];
		if(temporarySum > leftSum) {
			leftSum = temporarySum;
		}
	}

	temporarySum = 0;
	int rightSum = INT_MIN;
	for(int i = middleIndex+1;i <= lastIndex;++i) {
		temporarySum = temporarySum + arr[i];
		if(temporarySum > rightSum) {
			rightSum = temporarySum;
		}
	}

	return leftSum + rightSum;
}

int getMaximumSubarraySum(int arr[],int firstIndex,int lastIndex) {
	if(firstIndex == lastIndex) {
		return arr[firstIndex];
	}

	int middleIndex = (firstIndex + lastIndex)/2;
	return getMaximumOfThree(
			getMaximumSubarraySum(arr, firstIndex, middleIndex),
			getMaximumSubarraySum(arr, middleIndex+1, lastIndex),
			getMaximumCrossingSum(arr, firstIndex, middleIndex, lastIndex)
	);
}

int main() {
	int arr[] = {2, 3, 4, 5, 7};
	int length = sizeof(arr)/sizeof(arr[0]);
	int maximumSubarraySum = getMaximumSubarraySum(arr, 0, length-1);
	cout << "Maximum contiguous sum is: " << maximumSubarraySum << endl;
	return 0;
}
```

#### Time Complexity
`getMaximumSubarraySum()` is a recursive method and time complexity can be expressed as following recurrence relation.
```
T(n) = 2T(n/2) + Θ(n)
```
The above recurrence is similar to Merge Sort and can be solved either using Recurrence Tree method or Master method. It falls in case II of Master Method and solution of the recurrence is `Θ(nLogn)`.

## Comparison with Kadane Algorithm
The [Kadane Algorithm](https://jalever.github.io/2019/07/01/Largest-Sum-Contiguous-Subarray/) for this problem takes `O(n)` time. Therefore the Kadane’s algorithm is better than the Divide and Conquer approach, but this problem can be considered as a good example to show power of Divide and Conquer.
