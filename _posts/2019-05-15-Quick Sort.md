---
layout: post
title: Sorting: Quick Sort
subtitle: Data Structure Sorting学习笔记系列
date: 2019-05-15
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
- Not Stable
- In-Place
- Best Case: O(n * log(n))
- Average Case: O(n * log(n))
- Worst Case: O( n^2 )

## Diagram
[![V2jRcn.md.png](https://s2.ax1x.com/2019/06/12/V2jRcn.md.png)](https://imgchr.com/i/V2jRcn)

[![V2jWXq.md.png](https://s2.ax1x.com/2019/06/12/V2jWXq.md.png)](https://imgchr.com/i/V2jWXq)

[![V2j4BV.md.png](https://s2.ax1x.com/2019/06/12/V2j4BV.md.png)](https://imgchr.com/i/V2j4BV)


## Implementation in CPP
```cpp
#include <bits/stdc++.h>
using namespace std;

void swap(int* a,int* b) {
	int temp = *a;
	*a = *b;
	*b = temp;
}

void traverseArray(int arr[],int length) {
	for(int i = 0;i < length;++i) {
		cout << arr[i] << "\t";
	}
}

int partition(int arr[],int low,int high) {
	int i = low - 1;
	int pivot = arr[high];

	for(int j = low;j < high;++j) {
		if(arr[j] <= pivot) {
			++i;
			swap(&arr[i], &arr[j]);
		}
	}

	swap(&arr[i+1], &arr[high]);
	return i+1;
}

void Sort(int arr[],int low,int high) {
	if(low < high) {
		int pi = partition(arr, low, high);
		Sort(arr,low, pi-1);
		Sort(arr, pi+1, high);
	}
}

int main() {
	int arr[] = {90,23,101,45,65,23,67,89,34,23};
	int length = sizeof(arr)/sizeof(arr[0]);
	cout << "Original Array: " << endl;
	traverseArray(arr, length);

	Sort(arr,0,length-1);

	cout << "\nSorted Array: " << endl;
	traverseArray(arr, length);

	return 0;
}

```

## Links
[Origin Article](https://www.geeksforgeeks.org/quick-sort/)
