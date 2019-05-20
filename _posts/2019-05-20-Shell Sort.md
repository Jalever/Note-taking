---
layout: post
title: Shell Sort
subtitle: Data Structure学习笔记系列
date: 2019-05-20
author: Jalever
header-img: img/post_2019_react_contextAPI_bg.png
catalog: true
tags:
  - Data Structure
---


## Features
- Average Case: O( n^2 )


```c
#include <stdio.h>

void shellSort(int arr[], int len) {
    for(int gap = len/2; gap > 0; gap = gap/2) {
        for(int i = gap;i < len;i++) {
            int temp = arr[i];

            int j;
            for(j = i;j >= gap && arr[j-gap] > temp;j = j - gap) {
                arr[j] = arr[j-gap];
            }
            arr[j] = temp;
        }
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

    shellSort(arr, n);
  
    printf("\nArray after sorting: \n");
    printArray(arr, n);

    return 0;
}

```
