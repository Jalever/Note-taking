---
layout: post
title: (DS Array)Array Rotations
subtitle: Data Structure Array Rotations
date: 2019-06-08
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Data Structure
---

## Program for array rotation
#### Overview
Write a function `rotate(ar[], d, n)` that rotates `arr[]` of size `n` by `d` elements
![VcY9vd.png](https://s2.ax1x.com/2019/06/11/VcY9vd.png)
Rotation of the above array by `2` will make array
![VcYQrn.png](https://s2.ax1x.com/2019/06/11/VcYQrn.png)

#### Juggling Algorithm
Instead of moving one by one, divide the array in different sets
where number of sets is equal to GCD of n and d and move the elements within sets.
If GCD is `1` as is for the above example array (`n = 7` and `d =2`), then elements will be moved within one set only, we just start with `temp = arr[0]` and keep moving `arr[I+d]` to `arr[I]` and finally store temp at the right place.

#### Diagram
![Vcb3cT.png](https://s2.ax1x.com/2019/06/11/Vcb3cT.png)

#### General
- Greatest Common Divisor
    - In mathematics, the greatest common divisor (gcd) of two or more integers, which are not all zero, is the largest positive integer that divides each of the integers. For example, the gcd of 8 and 12 is 4.
    - ![VcbyuD.png](https://s2.ax1x.com/2019/06/11/VcbyuD.png)
- Euclid Algorithm
    - Euclidean algorithm uses a division algorithm such as long division in combination with the observation that the gcd of two numbers also divides their difference. To compute gcd(48,18), divide 48 by 18 to get a quotient of 2 and a remainder of 12. Then divide 18 by 12 to get a quotient of 1 and a remainder of 6. Then divide 12 by 6 to get a remainder of 0, which means that 6 is the gcd.

#### Implementation
![evq3U1.png](https://s2.ax1x.com/2019/08/11/evq3U1.png)
![evqJC6.png](https://s2.ax1x.com/2019/08/11/evqJC6.png)
![evqtgO.png](https://s2.ax1x.com/2019/08/11/evqtgO.png)
```cpp
#include <iostream>

using namespace std;

int getGCD(int a,int b) {
	if(b == 0) {
		return a;
	}

	return getGCD(b, a%b);
}

void Traversal(int arr[], int length) {
    for (int i = 0; i < length; i++)
        cout << arr[i] << " ";
}

void Rotate(int arr[],int length,int gap) {
	int gcd = ::getGCD(length, gap);

	for(int i = 0;i < gcd;i++) {
		int temp = arr[i];
		int previousRoundIndex = i;

		while(1) {
			int nextRoundIndex = previousRoundIndex + gap;

			if(nextRoundIndex >= length) {
				nextRoundIndex -= length;
			}

			if(nextRoundIndex == i) {
				break;
			}

			arr[previousRoundIndex] = arr[nextRoundIndex];
			previousRoundIndex = nextRoundIndex;
		}

		arr[previousRoundIndex] = temp;
	}
}

int main() {
	int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
	int length = sizeof(arr) / sizeof(arr[0]);
	::Rotate(arr, length, 2);
	::Traversal(arr, length);

    return 0;
}
```

###### Time Complexity
Time complexity : O(n)

###### Auxiliary Space
Auxiliary Space : O(1)
