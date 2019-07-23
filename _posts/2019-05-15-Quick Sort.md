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
