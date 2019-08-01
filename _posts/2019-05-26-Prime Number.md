---
layout: post
title: Prime Number
subtitle: Mathematical Algorithms
date: 2019-05-26
author: Jalever
header-img: img/math_bg_simple.png
catalog: true
tags:
  - Mathematics
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
<mark><del>4</del></mark>&nbsp;
5&nbsp;
<mark><del>6</del></mark>&nbsp;
7&nbsp;
<mark><del>8</del></mark>&nbsp;
9&nbsp;
<mark><del>10</del></mark>&nbsp;
11&nbsp;
<mark><del>12</del></mark>&nbsp;
13&nbsp;
<mark><del>14</del></mark>&nbsp;
15&nbsp;
<mark><del>16</del></mark>&nbsp;
17&nbsp;
<mark><del>18</del></mark>&nbsp;
19&nbsp;
<mark><del>20</del></mark>&nbsp;
21&nbsp;
<mark><del>22</del></mark>&nbsp;
23&nbsp;
<mark><del>24</del></mark>&nbsp;
25&nbsp;
<mark><del>26</del></mark>&nbsp;
27&nbsp;
<mark><del>28</del></mark>&nbsp;
29&nbsp;
<mark><del>30</del></mark>&nbsp;
</p>

The next number in the list after 2 is 3; cross out every 3rd number in the list after 3 by counting up from 3 in increments of 3 (these will be all the multiples of 3 in the list):

Multiples of 3 would be deleted,for example: 6, 9, 12, 15, 18, 21, 24, 27, 30
<p>
2&nbsp;
3&nbsp;
<mark><del>4</del></mark>&nbsp;
5&nbsp;
<mark><del>6</del></mark>&nbsp;
7&nbsp;
<mark><del>8</del></mark>&nbsp;
<mark><del>9</del></mark>&nbsp;
<mark><del>10</del></mark>&nbsp;
11&nbsp;
<mark><del>12</del></mark>&nbsp;
13&nbsp;
<mark><del>14</del></mark>&nbsp;
<mark><del>15</del></mark>&nbsp;
<mark><del>16</del></mark>&nbsp;
17&nbsp;
<mark><del>18</del></mark>&nbsp;
19&nbsp;
<mark><del>20</del></mark>&nbsp;
<mark><del>21</del></mark>&nbsp;
<mark><del>22</del></mark>&nbsp;
23&nbsp;
<mark><del>24</del></mark>&nbsp;
25&nbsp;
<mark><del>26</del></mark>&nbsp;
<mark><del>27</del></mark>&nbsp;
<mark><del>28</del></mark>&nbsp;
29&nbsp;
<mark><del>30</del></mark>&nbsp;
</p>

The next number not yet crossed out in the list after 3 is 5; cross out every 5th number in the list after 5 by counting up from 5 in increments of 5 (i.e. all the multiples of 5):

Multiples of 5 would be deleted,for example: 10, 15, 20, 25, 30
<p>
2&nbsp;
3&nbsp;
<mark><del>4</del></mark>&nbsp;
5&nbsp;
<mark><del>6</del></mark>&nbsp;
7&nbsp;
<mark><del>8</del></mark>&nbsp;
<mark><del>9</del></mark>&nbsp;
<mark><del>10</del></mark>&nbsp;
11&nbsp;
<mark><del>12</del></mark>&nbsp;
13&nbsp;
<mark><del>14</del></mark>&nbsp;
<mark><del>15</del></mark>&nbsp;
<mark><del>16</del></mark>&nbsp;
17&nbsp;
<mark><del>18</del></mark>&nbsp;
19&nbsp;
<mark><del>20</del></mark>&nbsp;
<mark><del>21</del></mark>&nbsp;
<mark><del>22</del></mark>&nbsp;
23&nbsp;
<mark><del>24</del></mark>&nbsp;
<mark><del>25</del></mark>&nbsp;
<mark><del>26</del></mark>&nbsp;
<mark><del>27</del></mark>&nbsp;
<mark><del>28</del></mark>&nbsp;
29&nbsp;
<mark><del>30</del></mark>&nbsp;
</p>

The next number not yet crossed out in the list after 5 is 7; the next step would be to cross out every 7th number in the list after 7, but they are all already crossed out at this point, as these numbers (14, 21, 28) are also multiples of smaller primes because 7 × 7 is greater than 30. The numbers not crossed out at this point in the list are all the prime numbers below 30:

<p>
2&nbsp;
3&nbsp;
&nbsp;
5&nbsp;
&nbsp;
7&nbsp;
&nbsp;
&nbsp;
&nbsp;
11&nbsp;
&nbsp;
13&nbsp;
&nbsp;
&nbsp;
&nbsp;
17&nbsp;
&nbsp;
19&nbsp;
&nbsp;
&nbsp;
&nbsp;
23&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
29&nbsp;
&nbsp;
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
