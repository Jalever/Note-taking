---
layout: post
title: Ugly Number
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
    - [Simple Method](#simple-method)
    - [Implementation in Dynamical Programming](#implementation-in-dynamical-programming)
        - [Time Complexity](#time-complexity)
        - [Auxiliary Space](#auxiliary-space)

## Overview
Ugly numbers are numbers whose only prime factors are `2`, `3` or `5`. The sequence `1, 2, 3, 4, 5, 6, 8, 9, 10, 12, 15, …` shows the first 11 ugly numbers. By convention, `1` is included.

Given a number `n`, the task is to find `n`’th Ugly number.
![Z5l3Bq.png](https://s2.ax1x.com/2019/07/14/Z5l3Bq.png)


## Implementation in CPP
#### Simple Method
Loop for all positive integers until ugly number count is smaller than `n`, if an integer is ugly than increment ugly number count.

To check if a number is ugly, divide the number by greatest divisible powers of `2`, `3` and `5`, if the number becomes `1` then it is an ugly number otherwise not.

For example, let us see how to check for `300` is ugly or not. Greatest divisible power of `2` is `4`, after dividing `300` by `4` we get `75`. Greatest divisible power of `3` is `3`, after dividing `75` by `3` we get `25`. Greatest divisible power of `5` is `25`, after dividing `25` by `25` we get `1`. Since we get `1` finally, `300` is ugly number.

```cpp
#include <iostream>
using namespace std;

int MaxDivide(int a,int b) {
	while(a%b == 0) {
		a = a/b;
	}

	return a;
}

bool isUglyNumber(int value) {

	value = ::MaxDivide(value, 2);
	value = ::MaxDivide(value, 3);
	value = ::MaxDivide(value, 5);

	return (value == 1) ? true : false;
}

int getUglyNumber(int count) {
	int index = 1;
	int uglyNumberCount = 1;

	while(uglyNumberCount < count) {
		index++;
		if(isUglyNumber(index)) {
			uglyNumberCount++;
		}
	}

	return index;
}

int main() {
	int number,index;

	cout << "Please input a number: ";
	cin >> number;

	index = ::getUglyNumber(number);
	cout << "Output: " << index << endl;

	return 0;
}

```
This method is not time efficient as it checks for all integers until ugly number count becomes `n`, but space complexity of this method is `O(1)`

#### Implementation in Dynamical Programming
Here is a time efficient solution with `O(n)` extra space. The ugly-number sequence is `1, 2, 3, 4, 5, 6, 8, 9, 10, 12, 15, …`

because every number can only be divided by `2, 3, 5`, one way to look at the sequence is to split the sequence to three groups as below:

![Z5l6UK.png](https://s2.ax1x.com/2019/07/14/Z5l6UK.png)

We can find that every subsequence is the ugly-sequence itself `(1, 2, 3, 4, 5, …)` multiply `2`, `3`, `5`. Then we use similar merge method as merge sort, to get every ugly number from the three subsequence. Every step we choose the smallest one, and move one step after.
```text
1 Declare an array for ugly numbers:  ugly[n]
2 Initialize first ugly no:  ugly[0] = 1
3 Initialize three array index variables i2, i3, i5 to point to
   1st element of the ugly array:
        i2 = i3 = i5 =0;
4 Initialize 3 choices for the next ugly no:
         next_mulitple_of_2 = ugly[i2]*2;
         next_mulitple_of_3 = ugly[i3]*3
         next_mulitple_of_5 = ugly[i5]*5;
5 Now go in a loop to fill all ugly numbers till 150:
For (i = 1; i < 150; i++ )
{
    /* These small steps are not optimized for good
      readability. Will optimize them in C program */
    next_ugly_no  = Min(next_mulitple_of_2,
                        next_mulitple_of_3,
                        next_mulitple_of_5);

    ugly[i] =  next_ugly_no       

    if (next_ugly_no  == next_mulitple_of_2)
    {             
        i2 = i2 + 1;        
        next_mulitple_of_2 = ugly[i2]*2;
    }
    if (next_ugly_no  == next_mulitple_of_3)
    {             
        i3 = i3 + 1;        
        next_mulitple_of_3 = ugly[i3]*3;
     }            
     if (next_ugly_no  == next_mulitple_of_5)
     {    
        i5 = i5 + 1;        
        next_mulitple_of_5 = ugly[i5]*5;
     }

}/* end of for loop */
6.return next_ugly_no
```

Let us see how it works

```text
initialize
   ugly[] =  | 1 |
   i2 =  i3 = i5 = 0;

First iteration
   ugly[1] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
            = Min(2, 3, 5)
            = 2
   ugly[] =  | 1 | 2 |
   i2 = 1,  i3 = i5 = 0  (i2 got incremented )

Second iteration
    ugly[2] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
             = Min(4, 3, 5)
             = 3
    ugly[] =  | 1 | 2 | 3 |
    i2 = 1,  i3 =  1, i5 = 0  (i3 got incremented )

Third iteration
    ugly[3] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
             = Min(4, 6, 5)
             = 4
    ugly[] =  | 1 | 2 | 3 |  4 |
    i2 = 2,  i3 =  1, i5 = 0  (i2 got incremented )

Fourth iteration
    ugly[4] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
              = Min(6, 6, 5)
              = 5
    ugly[] =  | 1 | 2 | 3 |  4 | 5 |
    i2 = 2,  i3 =  1, i5 = 1  (i5 got incremented )

Fifth iteration
    ugly[4] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
              = Min(6, 6, 10)
              = 6
    ugly[] =  | 1 | 2 | 3 |  4 | 5 | 6 |
    i2 = 3,  i3 =  2, i5 = 1  (i2 and i3 got incremented )

Will continue same way till I < 150
```

```cpp
#include <iostream>
using namespace std;

int getMinimum(int a,int b) {
	return (a < b) ? a : b;
}

int getMinimumOfThree(int a,int b,int c) {
	return getMinimum(a, getMinimum(b, c));
};

int getUglyNumber(int number) {
	unsigned UglyNumberArray[number];
	unsigned nextUglyNumberOf2 = 2, nextUglyNumberOf3 = 3, nextUglyNumberOf5 = 5;
	unsigned index2 = 0, index3 = 0, index5 = 0;
	unsigned uglyNumber = 1;

	UglyNumberArray[0] = 1;

	for(int i = 1;i < number;i++) {
		uglyNumber = ::getMinimumOfThree(nextUglyNumberOf2, nextUglyNumberOf3, nextUglyNumberOf5);

		UglyNumberArray[i] = uglyNumber;

		if(uglyNumber == nextUglyNumberOf2) {
			index2 += 1;
			nextUglyNumberOf2 = UglyNumberArray[index2]*2;
		}

		if(uglyNumber == nextUglyNumberOf3) {
			index3 += 1;
			nextUglyNumberOf3 = UglyNumberArray[index3]*3;
		}

		if(uglyNumber == nextUglyNumberOf5) {
			index5 += 1;
			nextUglyNumberOf5 = UglyNumberArray[index5]*5;
		}
	}

	return uglyNumber;
}

int main() {
	int number,index;

	cout << "Please input a number: ";
	cin >> number;

	index = ::getUglyNumber(number);
	cout << "Output: " << index << endl;

	return 0;
}
```
###### Time Complexity
Time Complexity: O(n)

###### Auxiliary Space
Auxiliary Space: O(n)
