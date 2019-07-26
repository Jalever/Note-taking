---
layout: post
title: (DS Sorting)Insertion Sort
subtitle: Data Structure Sorting
date: 2019-05-18
author: Jalever
header-img: img/post-bg-business-sketchees.jpg
catalog: true
tags:
  - Data Structure
---
- [Features](#features)
- [Diagram](#diagram)
- [Implementation in CPP](#implementation-in-cpp)
- [Links](#links)

## Features
- In-Place
- Stable
- Average Case: O( n^2 )

## Attention
![VW7oQ0.png](https://s2.ax1x.com/2019/06/13/VW7oQ0.png)

## Implementation in CPP
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

## Links
[Origin Article](https://www.geeksforgeeks.org/insertion-sort/)
