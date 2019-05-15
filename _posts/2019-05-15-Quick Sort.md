---
layout: post
title: Quick Sort
subtitle: Data Structure学习笔记系列
date: 2019-05-15
author: Jalever
header-img: img/post_2019_react_contextAPI_bg.png
catalog: true
tags:
  - Data Structure
---

```c
#include<stdio.h>

void swap(int* a, int* b)
{
	int t = *a;
	*a = *b;
	*b = t;
}

int partition (int arr[], int low, int high)
{
	int pivot = arr[high];
	int i = low - 1;

	for (int j = low; j <= high- 1; j++)
	{
		if (arr[j] <= pivot)
		{
          	i++;
			swap(&arr[i], &arr[j]);
		}
	}

	swap(&arr[i + 1], &arr[high]);

	return (i + 1);
}

void quickSort(int arr[], int low, int high)
{
	if (low < high)
	{
		int pi = partition(arr, low, high);

		quickSort(arr, low, pi - 1);
		quickSort(arr, pi + 1, high);
	}
}

void printArray(int arr[], int size)
{
	int i;
	for (i=0; i < size; i++)
		printf("%d ", arr[i]);
	printf("\n");
}

int main()
{
	int arr[] = {10, 7, 8, 9, 1, 5};
	int n = sizeof(arr)/sizeof(arr[0]);

	quickSort(arr, 0, n-1);

	printf("Sorted array:");
	printArray(arr, n);

	return 0;
}
```

## Output
```
low = (0)arr[10], high = (5)arr[5]
pivot = 5
i = 0
for: (0)arr[10] <=> (4)arr[1]
unswap: high = arr[5](5)
finish: swap: arr[1](5) <=> arr[5](7)
pi = 1


low = (2)arr[8], high = (5)arr[7]
pivot = 7
unswap: high = arr[5](7)
finish: swap: arr[2](7) <=> arr[5](8)
pi = 2


low = (3)arr[9], high = (5)arr[8]
pivot = 8
unswap: high = arr[5](8)
finish: swap: arr[3](8) <=> arr[5](9)
pi = 3


low = (4)arr[10], high = (5)arr[9]
pivot = 9
unswap: high = arr[5](9)
finish: swap: arr[4](9) <=> arr[5](10)
pi = 4


Sorted array:1 5 7 8 9 10
```

## Time Complexity
average: O(n * log(n))
