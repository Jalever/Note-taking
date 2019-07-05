---
layout: post
title: (DS Array)Program for Array Rotation
subtitle: Array Rotations 1
date: 2019-06-08
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Data Structure
---

- [Overview](#overview)
- [Solutions](#solutions)
    - [Juggling Algorithm](#juggling-algorithm)
        - [Diagram](#diagram)
        - [General](#general)
        - [Implementation in CPP](#implementation-in-cpp)
        - [Time Complexity](#time-complexity)
        - [Auxiliary Space](#auxiliary-space)
- [Links](#links)


## Overview
Write a function rotate(ar[], d, n) that rotates arr[] of size n by d elements

![VcY9vd.png](https://s2.ax1x.com/2019/06/11/VcY9vd.png)

Rotation of the above array by 2 will make array

![VcYQrn.png](https://s2.ax1x.com/2019/06/11/VcYQrn.png)

## Solutions

#### Juggling Algorithm
Instead of moving one by one, divide the array in different sets
where number of sets is equal to GCD of n and d and move the elements within sets.
If GCD is 1 as is for the above example array (n = 7 and d =2), then elements will be moved within one set only, we just start with temp = arr[0] and keep moving arr[I+d] to arr[I] and finally store temp at the right place.

###### Diagram
![Vcb3cT.png](https://s2.ax1x.com/2019/06/11/Vcb3cT.png)

###### General

- Greatest Common Divisor
    - In mathematics, the greatest common divisor (gcd) of two or more integers, which are not all zero, is the largest positive integer that divides each of the integers. For example, the gcd of 8 and 12 is 4.
    - ![VcbyuD.png](https://s2.ax1x.com/2019/06/11/VcbyuD.png)
- Euclid Algorithm
    - Euclidean algorithm uses a division algorithm such as long division in combination with the observation that the gcd of two numbers also divides their difference. To compute gcd(48,18), divide 48 by 18 to get a quotient of 2 and a remainder of 12. Then divide 18 by 12 to get a quotient of 1 and a remainder of 6. Then divide 12 by 6 to get a remainder of 0, which means that 6 is the gcd.

###### Implementation in CPP
```cpp
#include <bits/stdc++.h>
using namespace std;

int getGreatestCommonDivisor(int length, int gap) {
	if(gap == 0) {
		return length;
	}

	return getGreatestCommonDivisor(gap, length%gap);
}

void jugglingAlgorithm(int arr[],int length, int gap) {
	int gcd = getGreatestCommonDivisor(length, gap);

	for(int i = 0;i < gcd;++i) {
		int temp = arr[i];
		int firstRoundIndex = i;

		while(1) {
			int nextRoundIndex = firstRoundIndex + gap;

			if(nextRoundIndex >= length) {
				nextRoundIndex = nextRoundIndex - length;
			}

			if(nextRoundIndex == i) {
				break;
			}

			arr[firstRoundIndex] = arr[nextRoundIndex];
			firstRoundIndex = nextRoundIndex;
		}

		arr[firstRoundIndex] = temp;
	}
}

void getArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        cout << arr[i] << " ";
}

int main() {
	int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
	    int length = sizeof(arr) / sizeof(arr[0]);
	    jugglingAlgorithm(arr, length, 2);
	    getArray(arr, length);

	    return 0;
}
```

###### Time Complexity
Time complexity : O(n)

###### Auxiliary Space
Auxiliary Space : O(1)

## Links
[Original Article Program for Array Rotation](https://www.geeksforgeeks.org/array-rotation/)
