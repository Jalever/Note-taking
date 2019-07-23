---
layout: post
title: (DS Sorting)Quick Sort
subtitle: Data Structure Sorting
date: 2019-05-15
author: Jalever
header-img: img/post-bg-business-sketchees.jpg
catalog: true
tags:
  - Data Structure
---
- [Overview](#overview)
- [Implementation in CPP](#implementation-in-cpp)

## Overview
<strong>Quicksort</strong>(sometimes called <strong>Partition-Exchange Sort</strong>) is an efficient sorting algorithm, serving as a systematic method for placing the elements of a Random Access File or an array in order. Developed by British computer scientist <strong>Tony Hoare</strong> in 1959 and published in 1961, it is still a commonly used algorithm for sorting. When implemented well, it can be about two or three times faster than its main competitors, <strong>Merge Sort</strong> and <strong>Heapsort</strong>.

Quicksort is a Comparison Sort, meaning that it can sort items of any type for which a "less-than" relation (formally, a total order) is defined. In efficient implementations it is <ins>not a Stable Sort</ins>, meaning that the relative order of equal sort items is not preserved. Quicksort can operate <ins>in-place</ins> on an array, requiring small additional amounts of memory to perform the sorting. It is very similar to Selection Sort, except that it does not always choose worst-case partition.

Mathematical analysis of quicksort shows that, on average, the algorithm takes <strong>O(n log n)</strong> comparisons to sort `n` items. In the worst case, it makes <strong>O(n2)</strong> comparisons, though this behavior is rare.

<table>
    <thead>
        <tr>
            <td colspan="2">Features</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Class</td>
            <td>Sorting Algorithm</td>
        </tr>
        <tr>
            <td>Worst-case performance</td>
            <td>O(n^2)</td>
        </tr>
        <tr>
            <td>Best-case performance</td>
            <td>O(n log n)(simple partition)<br/><br/>or O(n)(three-way partition and equal keys)</td>
        </tr>
        <tr>
            <td>Average performance</td>
            <td>O(n log n)</td>
        </tr>
        <tr>
            <td>Worst-case space complexity</td>
            <td>O(n) auxiliary (naive)<br/><br/>O(log n) auxiliary </td>
        </tr>
    </tbody>
</table>

## Implementation in CPP
![eFR2VS.png](https://s2.ax1x.com/2019/07/23/eFR2VS.png)
![eFRhCj.png](https://s2.ax1x.com/2019/07/23/eFRhCj.png)
![eFR48s.png](https://s2.ax1x.com/2019/07/23/eFR48s.png)
![eFRIvq.png](https://s2.ax1x.com/2019/07/23/eFRIvq.png)
```cpp
#include <iostream>

using namespace std;

void Swap(int* a,int* b) {
	int temp = *a;
	*a = *b;
	*b = temp;
}

void TraverseArray(int arr[],int length) {
	for(int i = 0;i < length;++i) {
		cout << arr[i] << "\t";
	}
}

int Partition(int arr[],int leftmostIndex,int rightmostIndex) {
	int pivot = arr[rightmostIndex];
	int pivotIndex = leftmostIndex - 1;

	for(int i=leftmostIndex;i < rightmostIndex;i++) {
		if(arr[i] <= pivot) {
			++pivotIndex;
			::Swap(&arr[i], &arr[pivotIndex]);
		}
	}

	::Swap(&arr[pivotIndex+1], &arr[rightmostIndex]);
	return pivotIndex+1;
}

void QuickSort(int arr[],int leftmostIndex, int rightmostIndex) {
	if(leftmostIndex < rightmostIndex) {
		int pivot = Partition(arr, leftmostIndex, rightmostIndex);
		::QuickSort(arr, leftmostIndex, pivot-1);
		::QuickSort(arr, pivot+1, rightmostIndex);
	}
}

int main() {
	int arr[] = {90,23,101,45,65,23,67,89,34,23};
	int length = sizeof(arr)/sizeof(arr[0]);
	cout << "Original Array: " << endl;
	TraverseArray(arr, length);

	QuickSort(arr,0,length-1);

	cout << "\nSorted Array: " << endl;
	TraverseArray(arr, length);

	return 0;
}
```

## Links
[Origin Article](https://www.geeksforgeeks.org/quick-sort/)
