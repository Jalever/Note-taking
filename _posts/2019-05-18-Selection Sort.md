---
layout: post
title: (DS Sorting)Selection Sort
subtitle: Data Structure学习笔记系列
date: 2019-05-18
author: Jalever
header-img: img/post-bg-business-sketchees.jpg
catalog: true
tags:
  - Data Structure
---

- [Features](#features)
- [Implementation in CPP](#implementation-in-cpp)
- [Links](#links)

## Features
- In-Place
- Stable
- Average Case: O( n^2 )

## Implementation in CPP
```c
void swap(int *xp, int *yp) {  
    int temp = *xp;  
    *xp = *yp;  
    *yp = temp;  
}  

void selectionSort(int arr[], int n) {  
    int i, j, min_idx;  

    for (i = 0; i < n-1; i++) {  
        min_idx = i;  

        for (j = i+1; j < n; j++) {
            if (arr[j] < arr[min_idx]){

                min_idx = j;  
            }
        }

        swap(&arr[min_idx], &arr[i]);  
    }  
}  

/* Function to print an array */
void printArray(int arr[], int size) {  
    int i;  
    for (i=0; i < size; i++){
        printf("%d  ", arr[i]);  
    }

}  

// Driver program to test above functions  
int main() {  
    int arr[] = {64, 25, 12, 22, 11};  
    int n = sizeof(arr)/sizeof(arr[0]);  
    selectionSort(arr, n);  
    printf("Sorted array: \n");
    printArray(arr, n);  
    return 0;  
}   
```

## Links
[Origin Article](https://www.geeksforgeeks.org/selection-sort/)
