---
layout: post
title: Merge Sort
subtitle: Data Structure学习笔记系列
date: 2019-05-20
author: Jalever
header-img: img/post_2019_react_contextAPI_bg.png
catalog: true
tags:
  - Data Structure
---


## Features
- Best Case: O( n * Log(n) )
- Average Case: O( n * Log(n) )
- Worst Case: O( n * Log(n) )


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

void printArray(int arr[], int n)
{
    for (int i=0; i<n; i++)
        printf("%d  ", arr[i]);
}

int main()
{
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
