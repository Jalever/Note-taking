---
layout: post
title: (DS Sorting)Merge Sort
subtitle: Data Structure Sorting
date: 2019-05-20
author: Jalever
header-img: img/post-bg-business-sketchees.jpg
catalog: true
tags:
  - Data Structure
---
- [Features](#features)
- [Common Errors](#common-errors)
- [Implementation in CPP](#implementation-in-cpp)
- [Links](#links)

## Features
- Best Case: O( n * Log(n) )
- Average Case: O( n * Log(n) )
- Worst Case: O( n * Log(n) )

## Common Errors
[![VRMU3j.md.png](https://s2.ax1x.com/2019/06/12/VRMU3j.md.png)](https://imgchr.com/i/VRMU3j)

[![VRMBD0.md.png](https://s2.ax1x.com/2019/06/12/VRMBD0.md.png)](https://imgchr.com/i/VRMBD0)

[![VRM4Dx.md.png](https://s2.ax1x.com/2019/06/12/VRM4Dx.md.png)](https://imgchr.com/i/VRM4Dx)

## Implementation in CPP
```c
#include <stdio.h>

void merge(int arr[], int leftIndex, int middleIndex, int rightIndex) {
    int leftLength = middleIndex - leftIndex + 1;
    int rightLength = rightIndex - middleIndex;
    int leftArray[leftLength],rightArray[rightLength];

    int leftSubArrayIndex, rightSubArrayIndex;
    for(leftSubArrayIndex = 0;leftSubArrayIndex < leftLength;leftSubArrayIndex++) {
        leftArray[leftSubArrayIndex] = arr[leftIndex + leftSubArrayIndex];
    }

    for(rightSubArrayIndex = 0;rightSubArrayIndex < rightLength;rightSubArrayIndex++) {
        rightArray[rightSubArrayIndex] = arr[middleIndex + 1 + rightSubArrayIndex];
    }

    leftSubArrayIndex = 0;
    rightSubArrayIndex = 0;
    int mergedSubArrayIndex = leftIndex;

    while(leftSubArrayIndex < leftLength && rightSubArrayIndex < rightLength) {
        if(leftArray[leftSubArrayIndex] <= rightArray[rightSubArrayIndex]) {
            arr[mergedSubArrayIndex] = leftArray[leftSubArrayIndex];
            leftSubArrayIndex++;
        } else {
            arr[mergedSubArrayIndex] = rightArray[rightSubArrayIndex];
            rightSubArrayIndex++;
        }

        mergedSubArrayIndex++;
    }

    while(leftSubArrayIndex < leftLength) {
        arr[mergedSubArrayIndex] = leftArray[leftSubArrayIndex];
        leftSubArrayIndex++;
        mergedSubArrayIndex++;
    }

    while(rightSubArrayIndex < rightLength) {
        arr[mergedSubArrayIndex] = rightArray[rightSubArrayIndex];
        rightSubArrayIndex++;
        mergedSubArrayIndex++;
    }
}

void mergeSort(int arr[], int leftIndex, int rightIndex) {
    if(leftIndex < rightIndex) {
        int middleIndex = leftIndex + (rightIndex - leftIndex)/2;

        mergeSort(arr, leftIndex, middleIndex);
        mergeSort(arr, middleIndex + 1, rightIndex);

        merge(arr, leftIndex, middleIndex, rightIndex);
    }
}

void printArray(int arr[], int n) {
    for (int i=0; i<n; i++)
        printf("%d  ", arr[i]);
}

int main() {
    int arr[] = {12, 34, 54, 2, 3}, i;
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Array before sorting: \n");
    printArray(arr, n);

    mergeSort(arr, 0, n-1);

    printf("\nArray after sorting: \n");
    printArray(arr, n);

    return 0;
}
```

## Links
[Origin Article](https://www.geeksforgeeks.org/merge-sort/)
