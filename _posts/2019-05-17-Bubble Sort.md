---
layout: post
title: Bubble Sort
subtitle: Data Structure学习笔记系列
date: 2019-05-17
author: Jalever
header-img: img/post_2019_react_contextAPI_bg.png
catalog: true
tags:
  - Data Structure
---

## Features
- In-Place
- Stable
- Best Case: O( n )
- Average Case: O( n^2 )
- Worst Case: O( n^2 )


```c
#include <stdio.h>

void swap (int *a, int *b) {
    int t = *a;
    *a = *b;
    *b = t;
}


void printArray(int arr[], int size) {
	int i;
	for (i=0; i < size; i++)
		printf("%d ", arr[i]);
	printf("\n");
}


void quickSort (int arr[], int len) {
    int flag = 0;
    for(int i = 0;i < len; i++) {
        flag = 0;

        for(int j = 0;j < len-i-1; j++) {
            if(arr[j] > arr[j+1]) {
                swap(&arr[j], &arr[j+1]);
                flag = 1;
            }
        }

        if(flag == 0) return;

    }

}

int main () {
    int arr[] = {10, 7, 8, 9, 1, 5};
	int n = sizeof(arr)/sizeof(arr[0]);

	quickSort(arr, n);

	printf("Sorted array:");
	printArray(arr, n);

  return 0;
}
```
