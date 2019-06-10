---
layout: post
title: Reversal Rotation
subtitle: Array Rotations学习笔记系列2
date: 2019-06-08
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
## Overview
Let AB are the two parts of the input array where A = arr[0..d-1] and B = arr[d..n-1]. The idea of the algorithm is :

- Reverse A to get ArB, where Ar is reverse of A.
- Reverse B to get ArBr, where Br is reverse of B.
- Reverse all to get (ArBr) r = BA.

## Source Codes

```cpp
#include<bits/stdc++.h>
using namespace std;

void printArray(int arr[],int length) {
    for(int i = 0;i < length;++i) {
        cout << arr[i] << "\t";
    }
}

void rotate(int arr[],int startIndex,int endIndex) {
    while(startIndex < endIndex) {
        int temp = arr[startIndex];
        arr[startIndex] = arr[endIndex];
        arr[endIndex] = temp;

        startIndex++;
        endIndex--;
    }
}

void reversalRotate(int arr[],int gap, int length) {
    rotate(arr, 0, gap-1);
    rotate(arr, gap, length-1);
    rotate(arr, 0, length-1);
}

int main() {
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};
    int length = sizeof(arr)/sizeof(arr[0]);
    int gap = 2;
    gap = gap % length;//in case the rotating factor is greater than array length

    reversalRotate(arr, gap, length);

    printArray(arr, length);
    return 0;
}
```

#### Time Complexity
Time Complexity : O(n)
