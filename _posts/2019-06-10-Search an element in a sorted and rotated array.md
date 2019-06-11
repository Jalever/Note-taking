---
layout: post
title: Search an element in a sorted and rotated array
subtitle: Array Rotations学习笔记系列5
date: 2019-06-08
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
Input  : arr[] = {5, 6, 7, 8, 9, 10, 1, 2, 3};<br/>
         key = 3<br/>
Output : Found at index 8<br/>

Input  : arr[] = {5, 6, 7, 8, 9, 10, 1, 2, 3};<br/>
         key = 30<br/>
Output : Not found<br/>

Input : arr[] = {30, 40, 50, 10, 20}<br/>
        key = 10<br/>
Output : Found at index 3

![Vc1hSs.png](https://s2.ax1x.com/2019/06/11/Vc1hSs.png)

```cpp
#include<iostream>
using namespace std;

int getKeyIndex(int arr[],int low,int high,int key) {
    if(low > high) {
        return -1;
    }

    int mid = (low + high)/2;

    if(key == arr[mid]) {
        return mid;
    }

    if(arr[mid] < key) {
        return getKeyIndex(arr, mid+1, high, key);
    } else {
        return getKeyIndex(arr, low, mid-1, key);
    }
}

int findPivot(int arr[],int low,int high) {
    if(low > high) {
        return -1;
    }

    if(low == high) {
        return low;
    }

    int mid = (low + high)/2;


    if(mid > low && arr[mid] < arr[mid-1]) {
        return mid-1;
    }

    if(mid < high && arr[mid] > arr[mid+1]) {
        return mid;
    }

    if(arr[low] >= arr[mid]) {
        return findPivot(arr,low, mid-1);
    } else {
        return findPivot(arr,mid+1,high);
    }
}

int getIndex(int arr[],int length,int key) {
    int pivot = findPivot(arr,0,length-1);

    if(pivot == -1) {
        return getKeyIndex(arr, 0, length-1, key);
    }

    if(arr[pivot] == key) {
        return pivot;
    }

    if(arr[0] <= key) {
        return getKeyIndex(arr,0,pivot-1,key);
    } else {
        return getKeyIndex(arr,pivot+1, length-1, key);
    }
}

void printArray(int arr[],int length) {
    for(int i = 0;i < length;++i) {
        cout << "[" << i << "]: " << arr[i] << "\n";
    }
    cout << endl;
}

int main()
{
  // Let us search 3 in below array
  int arr1[] = {5, 6, 7, 8, 9, 10, 1, 2, 3};
  int n = sizeof(arr1)/sizeof(arr1[0]);
  int key = 3;

    printArray(arr1, n);
  // Function calling
  cout << "Index of the element is : " << getIndex(arr1, n, key);

  return 0;
}

```


## Improved Solution
- Find middle point mid = (l + h)/2
- If key is present at middle point, return mid.
- Else If arr[l..mid] is sorted
    - If key to be searched lies in range from arr[l] to arr[mid], recur for arr[l..mid].
    - Else recur for arr[mid+1..h]
- Else (arr[mid+1..h] must be sorted)
    - If key to be searched lies in range from arr[mid+1] to arr[h], recur for arr[mid+1..h].
    - Else recur for arr[l..mid]

```cpp
#include<iostream>
using namespace std;

int getIndex(int arr[],int low, int high, int key) {
    if(low > high) {
        return -1;
    }

    int mid = (low + high)/2;

    if(arr[mid] == key) {
        return mid;
    }

    if(arr[low] <= arr[mid]) {
        if(key >= arr[low] && key <= arr[mid]) {
            return getIndex(arr, low, mid-1, key);
        }

        return getIndex(arr, mid+1, high, key);
    }

    if(key >= arr[mid] && key <= arr[high]) {
        return getIndex(arr, mid+1, high, key);
    }

    return getIndex(arr, low, mid-1, key);
}

int main() {
	int arr[] = {4, 5, 6, 7, 8, 9, 1, 2, 3};
	int n = sizeof(arr)/sizeof(arr[0]);
	int key = 2;
	int i = getIndex(arr, 0, n-1, key);

	if (i != -1)
	cout << "Index: " << i << endl;
	else
	cout << "Key not found";
}
```
