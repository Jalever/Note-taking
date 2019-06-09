---
layout: post
title: Program for Array Rotation
subtitle: Algorithm学习笔记系列
date: 2019-06-08
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

## Overview
Write a function rotate(ar[], d, n) that rotates arr[] of size n by d elements

```cpp
1 2 3 4 5 6 7
```

Rotation of the above array by 2 will make array

```cpp
3 4 5 6 7 1 2
```

## Greatest Common Divisor
In mathematics, the greatest common divisor (gcd) of two or more integers, which are not all zero, is the largest positive integer that divides each of the integers. For example, the gcd of 8 and 12 is 4.

#### Euclid Algorithm
A much more efficient method is the Euclidean algorithm, which uses a division algorithm such as long division in combination with the observation that the gcd of two numbers also divides their difference. To compute gcd(48,18), divide 48 by 18 to get a quotient of 2 and a remainder of 12. Then divide 18 by 12 to get a quotient of 1 and a remainder of 6. Then divide 12 by 6 to get a remainder of 0, which means that 6 is the gcd.

## Juggling Algorithm
Instead of moving one by one, divide the array in different sets
where number of sets is equal to GCD of n and d and move the elements within sets.
If GCD is 1 as is for the above example array (n = 7 and d =2), then elements will be moved within one set only, we just start with temp = arr[0] and keep moving arr[I+d] to arr[I] and finally store temp at the right place.

Here is an example for n = 12 and d = 3. GCD is 3 and

```cpp
#include <bits/stdc++.h>
using namespace std;

int getGreatestCommonDivisor(int a,int b) {


    if(b == 0) {
        return a;
    } else {
        getGreatestCommonDivisor(b, a % b);
    }
}

void LeftRotation(int arr[],int gap,int length) {
    int greatestCommonDivisor = getGreatestCommonDivisor(length, gap);

    for(int i = 0;i < greatestCommonDivisor;++i) {

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


void printArray(int arr[], int size) {
	for (int i = 0; i < size; i++)
		cout << arr[i] << " ";
}

int main() {
	int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
	int n = sizeof(arr) / sizeof(arr[0]);

	LeftRotation(arr, 3, n);
	printArray(arr, n);

	return 0;
}
```

#### Time Complexity
Time complexity : O(n)

#### Auxiliary Space
Auxiliary Space : O(1)

## Links
[Original Article Program for Array Rotation](https://www.geeksforgeeks.org/array-rotation/)
