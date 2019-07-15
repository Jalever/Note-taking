---
layout: post
title: Catalan Number
subtitle: Dynamic Programming Paradigm
date: 2019-07-01
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
- [Overview](#overview)
- [Implementation in CPP](#implementation-in-cpp)
    - [Recursive Solution](#recursive-solution)
    - [Dynamic Programming Solution](#dynamic-programming-solution)
    - [Binomial Coeffient Solution](#binomial-coeffient-solution)

## Overview


## Implementation in CPP
#### Recursive Solution
Catalan numbers satisfy the following recursive formula.

![ZoY1bQ.png](https://s2.ax1x.com/2019/07/15/ZoY1bQ.png)

Following is the implementation of above recursive formula.

```cpp
#include <iostream>
using namespace std;

unsigned long int Catalan(unsigned int n) {
	if(n <= 1) {
		return 1;
	}

	unsigned long int result = 0;

	for(unsigned int i = 0;i < n;i++) {
		result += Catalan(i) * Catalan(n-i-1);
	}

	return result;
}

int main() {
	int value;
	unsigned long int number;
	cout << "Please input a number: ";
	cin >> value;

	number = Catalan(value);
	cout << "The number is " << number << endl;

	return 0;
}
```

#### Dynamic Programming Solution
We can observe that the above recursive implementation does a lot of repeated work (we can the same by drawing recursion tree). Since there are overlapping subproblems, we can use dynamic programming for this. Following is a Dynamic programming based implementation .

```cpp
#include <iostream>
using namespace std;

unsigned long int Catalan(unsigned int n) {
	unsigned long int arr[n+1];
	arr[0] = arr[1] = 1;

	for(unsigned int i = 2;i <= n;i++) {
		arr[i] = 0;
		for(unsigned int j = 0;j < i;j++) {
			arr[i] += arr[j] * arr[i-j-1];
		}
	}

	return arr[n];
}

int main() {
	int value;
	unsigned long int number;
	cout << "Please input a number: ";
	cin >> value;

	number = Catalan(value);
	cout << "The number is " << number << endl;

	return 0;
}
```

<strong>Time Complexity</strong>: Time complexity of above implementation is `O(n2)`

## Binomial Coeffient Solution
The nth Catalan number is given directly in terms of binomial coefficients by

![ZoUsaQ.png](https://s2.ax1x.com/2019/07/15/ZoUsaQ.png)
```cpp
#include <iostream>
using namespace std;

unsigned long int BinomialCoeffient(unsigned int n,unsigned int k) {
	unsigned long int result = 1;

	if(k > n - k) {
		k = n - k;
	}

	for(unsigned int i = 0;i < k;i++) {
		result *= (n-i);
		result /= (i+1);
	}

	return result;
}

unsigned long int Catalan(unsigned int n) {
	unsigned long int combination = ::BinomialCoeffient(2*n, n);

	return combination/(n+1);
}

int main() {
	unsigned long int  value;
	unsigned long int number;
	cout << "Please input a number: ";
	cin >> value;

	number = Catalan(value);
	cout << "The number is " << number << endl;

	return 0;
}
```
<strong>Time Complexity</strong>: Time complexity of above implementation is O(n).
