---
layout: post
title: Fibonacci Numbers
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
    - [Use Recursion](#use-recursion)
    - [Use Dynamical Programming](#use-dynamical-programming)
    - [Space Optimized Method 2](#space-optimized-method-2)
    - [Using the Power of the Matrix](#using-the-power-of-the-matrix)

## Overview
The Fibonacci numbers are the numbers in the following integer sequence.
`0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ……..`

In mathematical terms, the sequence `Fn` of Fibonacci numbers is defined by the recurrence relation
```text
Fn = Fn-1 + Fn-2
```

with seed values

```text
F0 = 0 and F1 = 1.
```

## Implementation in CPP
#### Use Recursion
A simple method that is a direct recursive implementation mathematical recurrence relation given above.

```cpp
#include <iostream>
using namespace std;

int Fibonacci(int n) {
	if(n <= 1) {
		return n;
	}

	return ::Fibonacci(n-1) + ::Fibonacci(n-2);
}

int main() {

	int value,number;
	cout << "Please input a number: ";
	cin >> value;

	number = Fibonacci(value);
	cout << "The number is " << number << endl;

	return 0;
}
```
<strong>Time Complexity</strong>: `T(n) = T(n-1) + T(n-2)` which is exponential.

<strong>Extra Space</strong>: `O(n)` if we consider the function call stack size, otherwise `O(1)`.

We can observe that this implementation does a lot of repeated work (see the following recursion tree). So this is a bad implementation for nth Fibonacci number.
![Z5YeNq.png](https://s2.ax1x.com/2019/07/14/Z5YeNq.png)

#### Use Dynamical Programming
We can avoid the repeated work done is the `Method 1` by storing the `Fibonacci Numbers` calculated so far.

```cpp
#include <iostream>
using namespace std;

int Fibonacci(int n) {
	int arr[n+2];

	arr[0] = 0;
	arr[1] = 1;

	for(int i = 2;i <= n;i++) {
		arr[i] = arr[i-1] + arr[i-2];
	}

	return arr[n];
}

int main() {

	int value,number;
	cout << "Please input a number: ";
	cin >> value;

	number = Fibonacci(value);
	cout << "The number is " << number << endl;

	return 0;
}
```

#### Space Optimized Method 2
We can optimize the space used in Method 2 by storing the previous two numbers only because that is all we need to get the next Fibonacci number in series.

```cpp
#include <iostream>
using namespace std;

int Fibonacci(int n) {
	int a = 0,b = 1, c;

	if(n == 0) {
		return a;
	}

	for(int i = 2;i <= n;i++) {

		c = a + b;
		a = b;
		b = c;
	}

	return b;
}

int main() {

	int value,number;
	cout << "Please input a number: ";
	cin >> value;

	number = Fibonacci(value);
	cout << "The number is " << number << endl;

	return 0;
}
```
<strong>Time Complexity</strong>:O(n)

<strong>Extra Space</strong>: O(1)

#### Using the Power of the Matrix
This another `O(n)` which relies on the fact that if we n times multiply the matrix `M = {{1,1},{1,0}}` to itself (in other words calculate power(M, n )), then we get the `(n+1)`th Fibonacci number as the element at row and column `(0, 0)` in the resultant matrix.

The matrix representation gives the following closed expression for the Fibonacci numbers:
![Z5sOuq.png](https://s2.ax1x.com/2019/07/14/Z5sOuq.png)

```cpp
#include <iostream>
using namespace std;

void Multiplication(int F[2][2],int M[2][2]) {
	int f1 = F[0][0] * M[0][0] + F[0][1] * M[1][0];
	int f2 = F[0][0] * M[0][1] + F[0][1] * M[1][1];
	int f3 = F[1][0] * M[0][0] + F[1][1] * M[1][0];
	int f4 = F[1][0] * M[0][1] + F[1][1] * M[1][1];

	F[0][0] = f1;
	F[0][1] = f2;
	F[1][0] = f3;
	F[1][1] = f4;
}

void Power(int F[2][2],int n) {
	int M[2][2] = {
			{1, 1},
			{1, 0}
	};

	for(int i = 2;i <= n;i++) {
		::Multiplication(F, M);
		cout << "F[0][0]" << F[0][0] << endl;
	}
}

int Fibonacci(int n) {
	int F[2][2] = {
		{1, 1},
		{1, 0}
	};

	if(n == 0) {
		return 0;
	}

	::Power(F, n-1);

	return F[0][0];
}

int main() {
	int value,number;
	cout << "Please input a number: ";
	cin >> value;

	number = Fibonacci(value);
	cout << "The number is " << number << endl;

	return 0;
}
```

<strong>Time Complexity</strong>:O(n)

<strong>Extra Space</strong>: O(1)
