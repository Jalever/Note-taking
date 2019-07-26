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

- [Features](#features)
- [Implementation in C](#implementation-in-c)
- [Pseudocode](#pseudocode)
- [Links](#links)

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
            <td>O(n2) (worst known worst case gap sequence)</td>
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
```cpp
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

## Links
[Origin Article](https://www.geeksforgeeks.org/shellsort/)
