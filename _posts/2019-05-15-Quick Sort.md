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
    - [Implementation issues](#implementation-issues)
        - [Choice of pivot](#choice-of-pivot)
        - [Repeated elements](#repeated-elements)
        - [Optimizations](#optimizations)
        - [Parallelization](#parallelization)
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
This scheme is attributed to <strong>Nico Lomuto</strong> and popularized by <strong>Bentley</strong> in his book <ins>Programming Pearls</ins> and Cormen et al. in their book <ins>Introduction to Algorithms</ins>. This scheme chooses a pivot that is typically the last element in the array. The algorithm maintains index `i` as it scans the array using another index `j` such that the elements `lo` through `i-1` (inclusive) are less than the pivot, and the elements `i` through `j` (inclusive) are equal to or greater than the pivot. As this scheme is more compact and easy to understand, it is frequently used in introductory material, although it is less efficient than Hoare's original scheme. This scheme degrades to `O(n^2)` when the array is already in order. There have been various variants proposed to boost performance including various ways to select pivot, deal with equal elements, use other sorting algorithms such as <strong>Insertion Sort</strong> for small arrays and so on. In pseudocode, a quicksort that sorts elements `lo` through `hi` (inclusive) of an array <strong>A</strong> can be expressed as:
![eEibjJ.png](https://s2.ax1x.com/2019/07/24/eEibjJ.png)
![eEiLu9.png](https://s2.ax1x.com/2019/07/24/eEiLu9.png)
Sorting the entire array is accomplished by <strong>Quicksort(A, 0, length&#40;A&#41; - 1)</strong>.

#### Hoare partition scheme
The original partition scheme described by <strong>C.A.R. Hoare</strong> uses two indices that start at the ends of the array being partitioned, then move toward each other, until they detect an inversion: a pair of elements, one greater than or equal to the pivot, one lesser or equal, that are in the wrong order relative to each other. The inverted elements are then swapped. When the indices meet, the algorithm stops and returns the final index. Hoare's scheme is more efficient than Lomuto's partition scheme because it does three times fewer swaps on average, and it creates efficient partitions even when all values are equal. Like Lomuto's partition scheme, Hoare's partitioning also would cause Quicksort to degrade to `O(n^2)` for already sorted input, if the pivot was chosen as the first or the last element. With the middle element as the pivot, however, sorted data results with (almost) no swaps in equally sized partitions leading to best case behavior of Quicksort, i.e. <strong>O(n log&#40;n&#41;)</strong>. Like others, Hoare's partitioning doesn't produce a stable sort. Note that in this scheme, the pivot's final location is not necessarily at the index that was returned, and the next two segments that the main algorithm recurs on are `(lo..p)` and `(p+1..hi)` as opposed to `(lo..p-1)` and `(p+1..hi)` as in Lomuto's scheme. However, the partitioning algorithm guarantees lo ≤ p < hi which implies both resulting partitions are non-empty, hence there's no risk of infinite recursion. In pseudocode,
![eEFu8S.png](https://s2.ax1x.com/2019/07/24/eEFu8S.png)
![eEFVEt.png](https://s2.ax1x.com/2019/07/24/eEFVEt.png)
The entire array is sorted by <strong>quicksort(A, 0, length&#40;A&#41;-1)</strong>.

#### Implementation issues
###### Choice of pivot
In the very early versions of quicksort, the leftmost element of the partition would often be chosen as the pivot element. Unfortunately, this causes worst-case behavior on already sorted arrays, which is a rather common use-case. The problem was easily solved by choosing either a random index for the pivot, choosing the middle index of the partition or (especially for longer partitions) choosing the median of the first, middle and last element of the partition for the pivot (as recommended by <strong>Sedgewick</strong>). This "median-of-three" rule counters the case of sorted (or reverse-sorted) input, and gives a better estimate of the optimal pivot (the true median) than selecting any single element, when no information about the ordering of the input is known.

Median-of-three code snippet for Lomuto partition:
![eEAe1S.png](https://s2.ax1x.com/2019/07/24/eEAe1S.png)
It puts a median into `A[hi]` first, then that new value of `A[hi]` is used for a pivot, as in a basic algorithm presented above.

Specifically, the expected number of comparisons needed to sort `n` elements with random pivot selection is `1.386 n log n`. Median-of-three pivoting brings this down to `Cn, 2 ≈ 1.188 n log n`, at the expense of a three-percent increase in the expected number of swaps. An even stronger pivoting rule, for larger arrays, is to pick the ninther, a recursive median-of-three (Mo3), defined as
![eEAM0s.png](https://s2.ax1x.com/2019/07/24/eEAM0s.png)
Selecting a pivot element is also complicated by the existence of Integer Overflow. If the boundary indices of the subarray being sorted are sufficiently large, the naïve expression for the middle index, `(lo + hi)/2`, will cause overflow and provide an invalid pivot index. This can be overcome by using, for example, `lo + (hi−lo)/2` to index the middle element, at the cost of more complex arithmetic. Similar issues arise in some other methods of selecting the pivot element.

###### Repeated elements
With a partitioning algorithm such as the Lomuto partition scheme described above (even one that chooses good pivot values), quicksort exhibits poor performance for inputs that contain many repeated elements. The problem is clearly apparent when all the input elements are equal: at each recursion, the left partition is empty (no input values are less than the pivot), and the right partition has only decreased by one element (the pivot is removed). Consequently, the Lomuto partition scheme takes <strong>Quadratic Time</strong> to sort an array of equal values. However, with a partitioning algorithm such as the Hoare partition scheme, repeated elements generally results in better partitioning, and although needless swaps of elements equal to the pivot may occur, the running time generally decreases as the number of repeated elements increases (with memory cache reducing the swap overhead). In the case where all elements are equal, Hoare partition scheme needlessly swaps elements, but the partitioning itself is best case, as noted in the Hoare partition section above.

To solve the Lomuto partition scheme problem(sometimes called the <strong>Dutch national flag problem</strong>), an alternative linear-time partition routine can be used that separates the values into three groups: values less than the pivot, values equal to the pivot, and values greater than the pivot. (Bentley and McIlroy call this a "fat partition" and note that it was already implemented in the <strong>qsort</strong> of Version 7 Unix.) The values equal to the pivot are already sorted, so only the less-than and greater-than partitions need to be recursively sorted. In pseudocode, the quicksort algorithm becomes
![eEAxNq.png](https://s2.ax1x.com/2019/07/24/eEAxNq.png)

The <strong>partition</strong> algorithm returns indices to the first ('leftmost') and to the last ('rightmost') item of the middle partition. Every item of the partition is equal to <strong>p</strong> and is therefore sorted. Consequently, the items of the partition need not be included in the recursive calls to <strong>quicksort</strong>.

The best case for the algorithm now occurs when all elements are equal (or are chosen from a small set of k ≪ n elements). In the case of all equal elements, the modified quicksort will perform only two recursive calls on empty subarrays and thus finish in linear time (assuming the <strong>partition</strong> subroutine takes no longer than linear time).

###### Optimizations
Two other important optimizations, also suggested by Sedgewick and widely used in practice, are:
- To make sure at most `O(log n)` space is used, recur first into the smaller side of the partition, then use a tail call to recur into the other, or update the parameters to no longer include the now sorted smaller side, and iterate to sort the larger side.
- When the number of elements is below some threshold (perhaps ten elements), switch to a non-recursive sorting algorithm such as Insertion Sort that performs fewer swaps, comparisons or other operations on such small arrays. The ideal 'threshold' will vary based on the details of the specific implementation.
- An older variant of the previous optimization: when the number of elements is less than the threshold `k`, simply stop; then after the whole array has been processed, perform insertion sort on it. Stopping the recursion early leaves the array k-sorted, meaning that each element is at most `k` positions away from its final sorted position. In this case, insertion sort takes `O(kn)` time to finish the sort, which is linear if `k` is a constant. Compared to the "many small sorts" optimization, this version may execute fewer instructions, but it makes suboptimal use of the Cache Memories in modern computers.

###### Parallelization
Quicksort's divide-and-conquer formulation makes it amenable to Parallelization using Task Parallelism. The partitioning step is accomplished through the use of a Parallel Prefix Sum algorithm to compute an index for each array element in its section of the partitioned array. Given an array of size `n`, the partitioning step performs `O(n)` work in `O(log n)` time and requires `O(n)` additional scratch space. After the array has been partitioned, the two partitions can be sorted recursively in parallel. Assuming an ideal choice of pivots, parallel quicksort sorts an array of size n in `O(n log n)` work in `O(log² n)` time using `O(n)` additional space.

Quicksort has some disadvantages when compared to alternative sorting algorithms, like <strong>Merge Sort</strong>, which complicate its efficient parallelization. The depth of quicksort's divide-and-conquer tree directly impacts the algorithm's scalability, and this depth is highly dependent on the algorithm's choice of pivot. Additionally, it is difficult to parallelize the partitioning step efficiently in-place. The use of scratch space simplifies the partitioning step, but increases the algorithm's memory footprint and constant overheads.

Other more sophisticated parallel sorting algorithms can achieve even better time bounds. For example, in 1991 David Powers described a parallelized quicksort (and a related <strong>Radix Sort</strong>) that can operate in `O(log n)` time on a CRCW (concurrent read and concurrent write) PRAM (parallel random-access machine)with n processors by performing partitioning implicitly.


#### Formal analysis
###### Worst-case analysis
The most unbalanced partition occurs when one of the sublists returned by the partitioning routine is of size <strong>n − 1</strong>. This may occur if the pivot happens to be the <strong>smallest</strong> or <strong>largest</strong> element in the list, or in some implementations (e.g., the Lomuto partition scheme as described above) when <strong>all the elements are equal</strong>.

If this happens repeatedly in every partition, then each recursive call processes a list of size one less than the previous list. Consequently, we can make <strong>n − 1</strong> nested calls before we reach a list of size <strong>1</strong>. This means that the Call Tree is a linear chain of <strong>n − 1</strong> nested calls. The ith call does <strong>O(n − i)</strong> work to do the partition, and
![emOySH.png](https://s2.ax1x.com/2019/07/26/emOySH.png)
,so in that case Quicksort takes <strong>O(n²)</strong> time.


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
