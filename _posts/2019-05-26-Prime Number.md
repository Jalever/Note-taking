---
layout: post
title: Prime Number
subtitle: Algorithm学习笔记系列
date: 2019-05-26
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

## Overview
A prime number (or a prime) is a natural number greater than 1 that cannot be formed by multiplying two smaller natural numbers.

A natural number greater than 1 that is not prime is called a composite number.

For example, 5 is prime because the only ways of writing it as a product, 1 × 5 or 5 × 1, involve 5 itself. However, 6 is composite because it is the product of two numbers (2 × 3) that are both smaller than 6.

## Eratosthenes's method
A prime number is a natural number that has exactly two distinct natural number divisors: 1 and itself.

To find all the prime numbers less than or equal to a given integer n by Eratosthenes' method:

1. Create a list of consecutive integers from 2 through n: (2, 3, 4, ..., n).
2. Initially, let p equal 2, the smallest prime number.
3. Enumerate the multiples of p by counting in increments of p from 2p to n, and mark them in the list (these will be 2p, 3p, 4p, ...; the p itself should not be marked).
4. Find the first number greater than p in the list that is not marked. If there was no such number, stop. Otherwise, let p now equal this new number (which is the next prime), and repeat from step 3.
5. When the algorithm terminates, the numbers remaining not marked in the list are all the primes below n.

The main idea here is that every value given to p will be prime, because if it were composite it would be marked as a multiple of some other, smaller prime. Note that some of the numbers may be marked more than once (e.g., 15 will be marked both for 3 and 5).

To find all the prime numbers less than or equal to 30, proceed as follows.

First, generate a list of integers from 2 to 30:
<p>
2&nbsp;
3&nbsp;
4&nbsp;
5&nbsp;
6&nbsp;
7&nbsp;
8&nbsp;
9&nbsp;
10&nbsp;
11&nbsp;
12&nbsp;
13&nbsp;
14&nbsp;
15&nbsp;
16&nbsp;
17&nbsp;
18&nbsp;
19&nbsp;
20&nbsp;
21&nbsp;
22&nbsp;
23&nbsp;
24&nbsp;
25&nbsp;
26&nbsp;
27&nbsp;
28&nbsp;
29&nbsp;
30&nbsp;
</p>

The first number in the list is 2; cross out every 2nd number in the list after 2 by counting up from 2 in increments of 2 (these will be all the multiples of 2 in the list)

Multiples of 2 would be deleted,for example: 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30
<p>
2&nbsp;
3&nbsp;
<del>4</del>&nbsp;
5&nbsp;
<del>6</del>&nbsp;
7&nbsp;
<del>8</del>&nbsp;
9&nbsp;
<del>10</del>&nbsp;
11&nbsp;
<del>12</del>&nbsp;
13&nbsp;
<del>14</del>&nbsp;
15&nbsp;
<del>16</del>&nbsp;
17&nbsp;
<del>18</del>&nbsp;
19&nbsp;
<del>20</del>&nbsp;
21&nbsp;
<del>22</del>&nbsp;
23&nbsp;
<del>24</del>&nbsp;
25&nbsp;
<del>26</del>&nbsp;
27&nbsp;
<del>28</del>&nbsp;
29&nbsp;
<del>30</del>&nbsp;
</p>

The next number in the list after 2 is 3; cross out every 3rd number in the list after 3 by counting up from 3 in increments of 3 (these will be all the multiples of 3 in the list):

Multiples of 3 would be deleted,for example: 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30
<p>
2&nbsp;
3&nbsp;
<del>4</del>&nbsp;
5&nbsp;
<del>6</del>&nbsp;
7&nbsp;
<del>8</del>&nbsp;
<del>9</del>&nbsp;
<del>10</del>&nbsp;
11&nbsp;
<del>12</del>&nbsp;
13&nbsp;
<del>14</del>&nbsp;
<del>15</del>&nbsp;
<del>16</del>&nbsp;
17&nbsp;
<del>18</del>&nbsp;
19&nbsp;
<del>20</del>&nbsp;
<del>21</del>&nbsp;
<del>22</del>&nbsp;
23&nbsp;
<del>24</del>&nbsp;
25&nbsp;
<del>26</del>&nbsp;
<del>27</del>&nbsp;
<del>28</del>&nbsp;
29&nbsp;
<del>30</del>&nbsp;
</p>


## Implementation in
```c
#include <stdio.h>
#include <math.h>

void prime(int len) {

    int arr[len];
    double squareRoot = sqrt(len);

    for(int i = 0;i < len;i++) {
        arr[i] = 1;
    }

    arr[0] = 0;
    arr[1] = 0;

    for(int i = 2;i < squareRoot;i++) {
        int n = 0;
        for(int j=i*i;j < len;j=i*i+n*i) {
            arr[j] = 0;
          	n++;
        }
    }

    for(int i = 0;i < len;i++) {
        if(arr[i] == 1) {
            printf("%d ", i);
        }
    }
}


int main()
{

    prime(30);

    return 0;
}
```
