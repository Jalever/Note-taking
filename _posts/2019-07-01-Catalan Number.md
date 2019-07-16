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
    - [Polygon Diagrams](#polygon-diagrams)
    - [Step Diagrams](#step-diagrams)
    - [Multiplication Diagrams](#multiplication-diagrams)
- [Implementation in CPP](#implementation-in-cpp)
    - [Recursive Solution](#recursive-solution)
    - [Dynamic Programming Solution](#dynamic-programming-solution)
    - [Binomial Coeffient Solution](#binomial-coeffient-solution)

## Overview
The Catalan numbers (1, 1, 2, 5, 14, 42, 132, 429, 1430, 4862, 16796, 58786, 208012, 742900, 2674440, 9694845, 35357670, 129644790, ...), named after <strong>Eugène Charles Catalan</strong>(1814–1894), arise in a number of problems in combinatorics.

They can be computed using this formula:
![ZoUsaQ.png](https://s2.ax1x.com/2019/07/15/ZoUsaQ.png)

Among other things, the Catalan numbers describe:
- the number of ways a polygon with `n+2` sides can be cut into n triangles
- the number of ways to use `n` rectangles to tile a stairstep shape (1, 2, ..., n−1, n).
- the number of ways in which parentheses can be placed in a sequence of numbers to be multiplied, two at a time
- the number of planar binary trees with `n+1` leaves
- the number of paths of length `2n` through an n-by-n grid that do not rise above the main diagonal

#### Polygon Diagrams
4 sides, 2 ways:
![ZoI9u8.png](https://s2.ax1x.com/2019/07/15/ZoI9u8.png)

5 sides, 5 ways:
![ZoIkNj.png](https://s2.ax1x.com/2019/07/15/ZoIkNj.png)

6 sides, 14 ways:
![ZoIA4s.png](https://s2.ax1x.com/2019/07/15/ZoIA4s.png)

7 sides, 42 ways:
![ZoIVCn.png](https://s2.ax1x.com/2019/07/15/ZoIVCn.png)

8 sides, 132 ways:
![ZoIZ3q.png](https://s2.ax1x.com/2019/07/15/ZoIZ3q.png)

#### Step Diagrams
2 rectangles, 2 ways:
![ZoIBUH.png](https://s2.ax1x.com/2019/07/15/ZoIBUH.png)

3 rectangles, 5 ways:
![ZoIy8I.png](https://s2.ax1x.com/2019/07/15/ZoIy8I.png)

4 rectangles, 14 ways:
![ZoI62t.png](https://s2.ax1x.com/2019/07/15/ZoI62t.png)

5 rectangles, 42 ways:
![ZoIRr8.png](https://s2.ax1x.com/2019/07/15/ZoIRr8.png)

6 rectangles, 132 ways:
![ZoILrT.png](https://s2.ax1x.com/2019/07/15/ZoILrT.png)

#### Multiplication Diagrams
3 numbers:
![ZooTTe.png](https://s2.ax1x.com/2019/07/15/ZooTTe.png)

4 numbers:
![Zooj6P.png](https://s2.ax1x.com/2019/07/15/Zooj6P.png)

5 numbers:
![ZoovOf.png](https://s2.ax1x.com/2019/07/15/ZoovOf.png)

6 numbers:
![ZoTCkQ.png](https://s2.ax1x.com/2019/07/15/ZoTCkQ.png)

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
<strong>Time Complexity</strong>: Time complexity of above implementation is `O(n)`.
