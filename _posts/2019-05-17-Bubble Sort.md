---
layout: post
title: (DS Sorting)Bubble Sort
subtitle: Data Structure Sorting
date: 2019-05-17
author: Jalever
header-img: img/post-bg-business-sketchees.jpg
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

## Implementation in CPP
```cpp
#include <iostream>
using namespace std;

void swap (int *a, int *b) {
    int t = *a;
    *a = *b;
    *b = t;
}

void printArray(int arr[], int size) {
	int i;
	for (i = 0; i < size; i++) {
		cout << arr[i] << " ";
	}

	cout << "\n" << endl;
}


void BubbleSort(int arr[], int len) {
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
	int length = sizeof(arr)/sizeof(arr[0]);

	BubbleSort(arr, length);

	cout << "Sorted array: " << endl;
	printArray(arr, length);

  return 0;
}
```
