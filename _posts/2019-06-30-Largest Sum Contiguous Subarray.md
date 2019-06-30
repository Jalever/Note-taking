---
layout: post
title: Largest Sum Contiguous Subarray
subtitle: Dynamic Programming学习笔记系列
date: 2019-06-30
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
- [Overview](#overview)
    - [Kadane Algorithm](#kadane-algorithm)
    - [Pseudo Codes](#pseudo-codes)
    - [Explanation](#explanation)
- [Implementation in CPP](#implementation-in-cpp)
    - [Implementation of Simple Sample](#implementation-of-simple-sample)
    - [Implementation of Optimized Sample](#implementation-of-optimized-sample)
    - [Implementation of Simple Sample](#implementation-of-simple-sample)
    - [Implementation with Index Range](#implementation-with-index-range)
    - [Time Complexity](#time-complexity)

## Overview
Write an efficient program to find the sum of contiguous subarray within a one-dimensional array of numbers which has the largest sum.
![ZlqdL8.png](https://s2.ax1x.com/2019/06/30/ZlqdL8.png)

## Kadane Algorithm
#### Pseudo Codes
```text
Initialize:
    sum = 0
    tempSum = 0

Loop for each element of the array
  (a) tempSum = tempSum + a[i]
  (b) if(tempSum < 0)
            tempSum = 0
  (c) if(sum < tempSum)
            sum = tempSum
return sum
```

#### Explanation
Simple idea of the Kadane’s algorithm is to look for all positive contiguous segments of the array (`tempSum` is used for this). And keep track of maximum sum contiguous segment among all positive segments (`sum` is used for this). Each time we get a positive sum compare it with `sum` and update `sum` if it is greater than `sum`
```text
Lets take the example:
    {-2, -3, 4, -1, -2, 1, 5, -3}

    sum = tempSum = 0

    for i=0,  a[0] =  -2
    tempSum = tempSum + (-2)
    Set tempSum = 0 because tempSum < 0

    for i=1,  a[1] =  -3
    tempSum = tempSum + (-3)
    Set tempSum = 0 because tempSum < 0

    for i=2,  a[2] =  4
    tempSum = tempSum + (4)
    tempSum = 4
    sum is updated to 4 because tempSum greater
    than sum which was 0 till now

    for i=3,  a[3] =  -1
    tempSum = tempSum + (-1)
    tempSum = 3

    for i=4,  a[4] =  -2
    tempSum = tempSum + (-2)
    tempSum = 1

    for i=5,  a[5] =  1
    tempSum = tempSum + (1)
    tempSum = 2

    for i=6,  a[6] =  5
    tempSum = tempSum + (5)
    tempSum = 7
    sum is updated to 7 because tempSum is
    greater than sum

    for i=7,  a[7] =  -3
    tempSum = tempSum + (-3)
    tempSum = 4
```

## Implementation in CPP
#### Implementation of Simple Sample
```cpp
#include <iostream>
#include <climits>

using namespace std;

int maxSubArraySum(int array[],int length) {
	int sum = INT_MIN, tempSum = 0;

	for(int i = 0;i < length;++i) {
		tempSum = tempSum + array[i];

		if(sum < tempSum) {
			sum = tempSum;
		}

		if(tempSum < 0) {
			tempSum = 0;
		}
	}

	return sum;
}

int main() {
	int array[] = {-2, -3, 4, -1, -2, 1, 5, -3};

	int length = sizeof(array)/sizeof(array[0]);

	int maxSum = ::maxSubArraySum(array, length);

	cout << "Maximum Contiguous Sum is: " << maxSum << endl;

	return 0;
}
```


#### Implementation of Optimized Sample
```cpp
#include <iostream>

using namespace std;

int maxSubArraySum_optimized(int array[],int length) {
	int sum = 0, tempSum = 0;

	for(int i = 0;i < length;++i) {
		tempSum = tempSum + array[i];

		if(tempSum < 0) {
			tempSum = 0;
		} else if(sum < tempSum) {
			sum = tempSum;
		}
	}

	return sum;
}

int main() {
	int array[] = {-2, -3, 4, -1, -2, 1, 5, -3};

	int length = sizeof(array)/sizeof(array[0]);

	int maxSum = ::maxSubArraySum_optimized(array, length);

	cout << "Maximum Contiguous Sum is: " << maxSum << endl;

	return 0;
}

```

#### Implementation of Simple Sample
```cpp
#include <iostream>

using namespace std;

int getMaximum(int a,int b) {
	return (a > b) ? a : b;
}

int maxSubArraySum_simple(int array[],int length) {
	int sum = array[0];
	int currentMax = array[0];

	for(int i = 1;i < length;++i) {
		currentMax = getMaximum(array[i], currentMax + array[i]);
		sum = getMaximum(currentMax, sum);
	}

	return sum;
}

int main() {
	int array[] = {-2, -3, 4, -1, -2, 1, 5, -3};

	int length = sizeof(array)/sizeof(array[0]);

	int maxSum = ::maxSubArraySum_simple(array, length);

	cout << "Maximum Contiguous Sum is: " << maxSum << endl;

	return 0;
}

```

#### Implementation with Index Range
```cpp
#include <iostream>
#include <climits>

using namespace std;

void maxSubArraySum_withIndex(int array[],int length) {
	int sum = INT_MIN, tempSum = 0;
	int startIndex = 0, endIndex = 0, tempStart = 0;

	for(int i = 0;i < length;++i) {
		tempSum = tempSum + array[i];

		if(sum < tempSum) {
			sum = tempSum;
			startIndex = tempStart;
			endIndex = i;
		}

		if(tempSum < 0) {
			tempSum = 0;
			tempStart = i + 1;
		}
	}

	cout << "Maximum Contiguous Sum is: " << sum << ", range: [" << startIndex << "] - [" << endIndex << "]" << endl;

}

int main() {
	int array[] = {-2, -3, 4, -1, -2, 1, 5, -3};

	int length = sizeof(array)/sizeof(array[0]);

	maxSubArraySum_withIndex(array, length);

	return 0;
}

```

#### Time Complexity
Time Complexity: `O(n)`
