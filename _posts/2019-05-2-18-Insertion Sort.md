---
layout: post
title: Insertion Sort
subtitle: Data Structure学习笔记系列
date: 2019-05-18
author: Jalever
header-img: img/post_2019_react_contextAPI_bg.png
catalog: true
tags:
  - Data Structure
---

## Features
- In-Place
- Stable
- Average Case: O( n^2 )


```c
#include <stdio.h>

void insertionSort(int arr[], int len) {


    for(int i = 1;i < len;i++) {

        int key = arr[i];
        int j = i - 1;

        while(j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }

        arr[j+1] = key;

    }

}

// A utility function to print an array of size n  
void printArray(int arr[], int n)  
{  
    int i;  
    for (i = 0; i < n; i++)  
        printf("%d ", arr[i]);
}  

/* Driver code */
int main()  
{  
    int arr[] = { 12, 11, 13, 5, 6 };  
    int n = sizeof(arr) / sizeof(arr[0]);  

    insertionSort(arr, n);  
    printArray(arr, n);  

    return 0;  
}  

```
