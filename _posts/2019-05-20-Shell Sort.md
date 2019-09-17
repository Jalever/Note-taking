---
layout: post
title: (DS Sorting)Shell Sort
subtitle: Data Structure Sorting
date: 2019-05-20
author: Jalever
header-img: img/post-bg-business-sketchees.jpg
catalog: true
tags:
  - Data Structure
---

- [Overview](#overview)
- [Features](#features)
- [Description](#description)
- [Pseudocode](#pseudocode)
- [Implementation in C](#implementation-in-c)

## Overview
<strong>Shellsort</strong>, also known as <strong>Shell sort</strong> or <strong>Shell's method</strong>, is an in-place Comparison Sort. It can be seen as either a generalization of sorting by exchange (Bubble Sort) or sorting by insertion (Insertion Sort). The method starts by sorting pairs of elements far apart from each other, then progressively reducing the gap between elements to be compared. Starting with far apart elements, it can move some out-of-place elements into position faster than a simple nearest neighbor exchange. Donald Shell published the first version of this sort in 1959. The running time of Shellsort is heavily dependent on the gap sequence it uses. For many practical variants, determining their time complexity remains an open problem.

## Features
<table>
    <thead>
        <tr style="textAlign: center">
            <td colspan="2">Shell Sort</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Class</td>
            <td>Sorting algorithm</td>
        </tr>
        <tr>
            <td>Data structure</td>
            <td>Array</td>
        </tr>
        <tr>
            <td>Worst-case performance</td>
            <td>O(n<sup>2</sup>) (worst known worst case gap sequence)</td>
        </tr>
        <tr>
            <td>Best-case performance</td>
            <td>O(n log n) (most gap sequences)</td>
        </tr>
        <tr>
            <td>Average performance</td>
            <td>depends on gap sequence</td>
        </tr>
        <tr>
            <td>Worst-case space complexity</td>
            <td>О(n) total, O(1) auxiliary</td>
        </tr>
    </tbody>
</table>

## Description
Shellsort is a generalization of Insertion Sort that allows the exchange of items that are far apart. The idea is to arrange the list of elements so that, starting anywhere, considering every `hth` element gives a sorted list. Such a list is said to be `h-sorted`. Equivalently, it can be thought of as `h` interleaved lists, each individually sorted. Beginning with large values of `h`, this rearrangement allows elements to move long distances in the original list, reducing large amounts of disorder quickly, and leaving less work for smaller `h-sort` steps to do. If the list is then `k-sorted` for some smaller integer `k`, then the list remains `h-sorted`. Following this idea for a decreasing sequence of `h` values ending in 1 is guaranteed to leave a sorted list in the end.

An example run of Shellsort with gaps `5`, `3` and `1` is shown below.
![eYnwdS.png](https://s2.ax1x.com/2019/07/31/eYnwdS.png)
The first pass, 5-sorting, performs insertion sort on five separate subarrays `(a1, a6, a11)`, `(a2, a7, a12)`, `(a3, a8)`, `(a4, a9)`, `(a5, a10)`. For instance, it changes the subarray `(a1, a6, a11)` from `(62, 17, 25)` to `(17, 25, 62)`. The next pass, 3-sorting, performs insertion sort on the three subarrays `(a1, a4, a7, a10)`, `(a2, a5, a8, a11)`, `(a3, a6, a9, a12)`. The last pass, 1-sorting, is an ordinary insertion sort of the entire array `(a1,..., a12)`.

As the example illustrates, the subarrays that Shellsort operates on are initially short; later they are longer but almost ordered. In both cases insertion sort works efficiently.

Shellsort is <strong>not stable</strong>: it may change the relative order of elements with equal values. It is an adaptive sorting algorithm in that it executes faster when the input is partially sorted.

## Pseudocode
```js
# Sort an array a[0...n-1].
gaps = [701, 301, 132, 57, 23, 10, 4, 1]

# Start with the largest gap and work down to a gap of 1
foreach (gap in gaps)
{
    # Do a gapped insertion sort for this gap size.
    # The first gap elements a[0..gap-1] are already in gapped order
    # keep adding one more element until the entire array is gap sorted
    for (i = gap; i < n; i += 1)
    {
        # add a[i] to the elements that have been gap sorted
        # save a[i] in temp and make a hole at position i
        temp = a[i]
        # shift earlier gap-sorted elements up until the correct location for a[i] is found
        for (j = i; j >= gap and a[j - gap] > temp; j -= gap)
        {
            a[j] = a[j - gap]
        }
        # put temp (the original a[i]) in its correct location
        a[j] = temp
    }
}
```

## Implementation in C
![eYnIJJ.png](https://s2.ax1x.com/2019/07/31/eYnIJJ.png)
![eYnTzR.png](https://s2.ax1x.com/2019/07/31/eYnTzR.png)
![eYnbsx.png](https://s2.ax1x.com/2019/07/31/eYnbsx.png)
```cpp
#include <iostream>

using namespace std;

void Shellsort(int arr[],int length) {
	for(int gap = length/2;gap > 0;gap = gap/2) {
		for(int i = gap;i < length;i++) {
			int temp = arr[i];

			int j;
			for(j = i;arr[j-gap] > temp && j >= gap;j -= gap) {
				arr[j] = arr[j-gap];
			}

			arr[j] = temp;
		}
	}
}

void Traversal(int arr[], int n) {
    for (int i=0; i<n; i++) {
        printf("%d ", arr[i]);
    }
}

int main() {
    int arr[] = {12, 34, 54, 84, 1, 321, 9, 2, 3};
    int length = sizeof(arr)/sizeof(arr[0]);

    cout << "Array before sorting: " << endl;
    ::Traversal(arr, length);

    ::Shellsort(arr, length);

    cout << "\nArray after sorting:" << endl;
    ::Traversal(arr, length);

    return 0;
}



```
