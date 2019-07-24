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
- [History](#history)
- [Algorithm](#algorithm)
    - [Lomuto partition scheme](#lomuto-partition-scheme)
    - [Hoare partition scheme](#hoare-partition-scheme)
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

## History
The quicksort algorithm was developed in 1959 by <strong>Tony Hoare</strong> while in the Soviet Union, as a visiting student at Moscow State University. At that time, Hoare worked on a project on Machine Translation for the National Physical Laboratory. As a part of the translation process, he needed to sort the words in Russian sentences prior to looking them up in a Russian-English dictionary that was already sorted in alphabetic order on magnetic tape. After recognizing that his first idea, <strong>Insertion Sort</strong>, would be slow, he quickly came up with a new idea that was <strong>Quicksort</strong>. He wrote a program in Mercury Autocode for the partition but could not write the program to account for the list of unsorted segments. On return to England, he was asked to write code for <strong>Shellsort</strong> as part of his new job. Hoare mentioned to his boss that he knew of a faster algorithm and his boss bet sixpence that he did not. His boss ultimately accepted that he had lost the bet. Later, Hoare learned about ALGOL and its ability to do recursion that enabled him to publish the code in <strong>Communications of the Association for Computing Machinery</strong>, the premier computer science journal of the time.

<strong>Quicksort</strong> gained widespread adoption, appearing, for example, in Unix as the default library sort subroutine. Hence, it lent its name to the C standard library subroutine <strong>qsort</strong> and in the reference implementation of Java.

<strong>Robert Sedgewick</strong>'s Ph.D. thesis in 1975 is considered a milestone in the study of Quicksort where he resolved many open problems related to the analysis of various pivot selection schemes including <strong>Samplesort</strong>, adaptive partitioning by <strong>Van Emden</strong> as well as derivation of expected number of comparisons and swaps. <strong>Bentley</strong> and <strong>McIlroy</strong> incorporated various improvements for use in programming libraries, including a technique to deal with equal elements and a pivot scheme known as <i>pseudomedian of nine</i>, where a sample of nine elements is divided into groups of three and then the median of the three medians from three groups is chosen. <strong>Jon Bentley</strong> described another simpler and compact partitioning scheme in his book <ins>Programming Pearls</ins> that he attributed to <strong>Nico Lomuto</strong>. Later Bentley wrote that he used Hoare's version for years but never really understood it but Lomuto's version was simple enough to prove correct. Bentley described Quicksort as the "most beautiful code I had ever written" in the same essay. Lomuto's partition scheme was also popularized by the textbook <ins>Introduction to Algorithms</ins> although it is inferior to Hoare's scheme because it does three times more swaps on average and degrades to `O(n^2)` runtime when all elements are equal.

In 2009, <strong>Vladimir Yaroslavskiy</strong> proposed the new dual pivot Quicksort implementation. In the Java core library mailing lists, he initiated a discussion claiming his new algorithm to be superior to the runtime library's sorting method, which was at that time based on the widely used and carefully tuned variant of classic Quicksort by Bentley and McIlroy. Yaroslavskiy's Quicksort has been chosen as the new default sorting algorithm in Oracle's Java 7 runtime library after extensive empirical performance tests.

## Algorithm
Quicksort is a <strong>Divide and Conquer</strong> algorithm. Quicksort first divides a large array into two smaller sub-arrays: the low elements and the high elements. Quicksort can then recursively sort the sub-arrays. The steps are:

1. Pick an element, called a <ins>pivot</ins>, from the array.
2. Partitioning: reorder the array so that all elements with values less than the pivot come before the pivot, while all elements with values greater than the pivot come after it (equal values can go either way). After this partitioning, the pivot is in its final position. This is called the <ins>partition</ins> operation.
3. Recursively apply the above steps to the sub-array of elements with smaller values and separately to the sub-array of elements with greater values.

The base case of the recursion is arrays of size zero or one, which are in order by definition, so they never need to be sorted.

The pivot selection and partitioning steps can be done in several different ways; the choice of specific implementation schemes greatly affects the algorithm's performance.
![eEiKmR.png](https://s2.ax1x.com/2019/07/24/eEiKmR.png)
Full example of quicksort on a random set of numbers. The shaded element is the <strong>pivot</strong>. It is always chosen as the last element of the partition. However, always choosing the last element in the partition as the pivot in this way results in poor performance <strong>&#40;O(n²)&#41;</strong> on already sorted arrays, or arrays of identical elements. Since sub-arrays of sorted/identical elements crop up a lot towards the end of a sorting procedure on a large set, versions of the quicksort algorithm that choose the pivot as the middle element run much more quickly than the algorithm described in this diagram on large sets of numbers.

#### Lomuto partition scheme
This scheme is attributed to <strong>Nico Lomuto</strong> and popularized by <strong>Bentley</strong> in his book <ins>Programming Pearls</ins> and Cormen et al. in their book <ins>Introduction to Algorithms</ins>. This scheme chooses a pivot that is typically the last element in the array. The algorithm maintains index `i` as it scans the array using another index `j` such that the elements `lo` through `i-1` (inclusive) are less than the pivot, and the elements `i` through `j` (inclusive) are equal to or greater than the pivot. As this scheme is more compact and easy to understand, it is frequently used in introductory material, although it is less efficient than Hoare's original scheme. This scheme degrades to `O(n^2)` when the array is already in order.[9] There have been various variants proposed to boost performance including various ways to select pivot, deal with equal elements, use other sorting algorithms such as <strong>Insertion Sort</strong> for small arrays and so on. In pseudocode, a quicksort that sorts elements `lo` through `hi` (inclusive) of an array <strong>A</strong> can be expressed as:
![eEibjJ.png](https://s2.ax1x.com/2019/07/24/eEibjJ.png)
![eEiLu9.png](https://s2.ax1x.com/2019/07/24/eEiLu9.png)
Sorting the entire array is accomplished by <strong>Quicksort(A, 0, length&#40;A&#41; - 1)</strong>.

#### Hoare partition scheme
The original partition scheme described by <strong>C.A.R. Hoare</strong> uses two indices that start at the ends of the array being partitioned, then move toward each other, until they detect an inversion: a pair of elements, one greater than or equal to the pivot, one lesser or equal, that are in the wrong order relative to each other. The inverted elements are then swapped. When the indices meet, the algorithm stops and returns the final index. Hoare's scheme is more efficient than Lomuto's partition scheme because it does three times fewer swaps on average, and it creates efficient partitions even when all values are equal. Like Lomuto's partition scheme, Hoare's partitioning also would cause Quicksort to degrade to `O(n^2)` for already sorted input, if the pivot was chosen as the first or the last element. With the middle element as the pivot, however, sorted data results with (almost) no swaps in equally sized partitions leading to best case behavior of Quicksort, i.e. <strong>O(n log&#40;n&#41;)</strong>. Like others, Hoare's partitioning doesn't produce a stable sort. Note that in this scheme, the pivot's final location is not necessarily at the index that was returned, and the next two segments that the main algorithm recurs on are `(lo..p)` and `(p+1..hi)` as opposed to `(lo..p-1)` and `(p+1..hi)` as in Lomuto's scheme. However, the partitioning algorithm guarantees lo ≤ p < hi which implies both resulting partitions are non-empty, hence there's no risk of infinite recursion. In pseudocode,
![eEFu8S.png](https://s2.ax1x.com/2019/07/24/eEFu8S.png)
![eEFVEt.png](https://s2.ax1x.com/2019/07/24/eEFVEt.png)
The entire array is sorted by <strong>quicksort(A, 0, length&#40;A&#41;-1)</strong>.



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
