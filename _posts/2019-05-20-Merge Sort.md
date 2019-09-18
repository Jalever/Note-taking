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
```cpp
#include <iostream>

using namespace std;

void Merge(int arr[],int leftIndex,int middleIndex,int rightIndex) {
	int leftLength = middleIndex - leftIndex + 1;
	int rightLength = rightIndex - middleIndex;

	int leftArray[leftLength], rightArray[rightLength];

	int leftSubIndex, rightSubIndex;
	for(leftSubIndex = 0;leftSubIndex < leftLength;leftSubIndex++) {
		leftArray[leftSubIndex] = arr[leftIndex + leftSubIndex];
	}

	for(rightSubIndex = 0;rightSubIndex < rightLength;rightSubIndex++) {
		rightArray[rightSubIndex] = arr[middleIndex + 1 + rightSubIndex];
	}

	leftSubIndex = 0;
	rightSubIndex = 0;
	int mergeIndex = leftIndex;

	while(leftSubIndex < leftLength && rightSubIndex < rightLength) {
		if(leftArray[leftSubIndex] <= rightArray[rightSubIndex]) {
			arr[mergeIndex] = leftArray[leftSubIndex];
			leftSubIndex++;
		} else {
			arr[mergeIndex] = rightArray[rightSubIndex];
			rightSubIndex++;
		}

		mergeIndex++;
	}

	while(leftSubIndex < leftLength) {
		arr[mergeIndex] = leftArray[leftSubIndex];
		mergeIndex++;
		leftSubIndex++;
	}

	while(rightSubIndex < rightLength) {
		arr[mergeIndex] = rightArray[rightSubIndex];
		mergeIndex++;
		rightSubIndex++;
	}
}

void Mergesort(int arr[],int leftIndex,int rightIndex) {
	if(leftIndex < rightIndex) {
		int middleIndex = leftIndex + (rightIndex - leftIndex)/2;

		::Mergesort(arr, leftIndex, middleIndex);
		::Mergesort(arr, middleIndex+1, rightIndex);

		::Merge(arr, leftIndex, middleIndex, rightIndex);
	}
}

void Traversal(int arr[], int n) {
    for (int i=0; i<n; i++)
        printf("%d ", arr[i]);
}

int main() {
    int arr[] = {12, 34, 43, 44,21,948, 1, 54, 2, 3};
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Array before sorting: \n");
    ::Traversal(arr, n);

    ::Mergesort(arr, 0, n-1);

    printf("\nArray after sorting: \n");
    ::Traversal(arr, n);

    return 0;
}

```

## Links
[Origin Article](https://www.geeksforgeeks.org/merge-sort/)
