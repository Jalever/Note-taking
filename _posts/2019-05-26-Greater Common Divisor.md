---
layout: post
title: Greater Common Divisor
subtitle: Mathematical Algorithms
date: 2019-05-26
author: Jalever
header-img: img/math_bg_simple.png
catalog: true
tags:
  - Mathematics
---

## Binary GCD Algorithm

## Implementation in C
```c
#include <stdio.h>
#include <math.h>

int gcd(int a, int b) {
    int exponent = 0;

    while(a%2 == 0 && b%2 == 0){
        a = a/2;
        b = b/2;
        exponent += 1;
    }

    while(a != b) {
        if(a%2 == 0) {
            a = a/2;
        } else if(b%2 == 0) {
            b = b/2;
        } else if(a > b) {
            a = (a - b)/2;
        } else {
            b =  (b - a)/2;
        }
    }

    int digit = a;

    return a * pow(2, exponent);
}

int main()
{
    int value = gcd(48, 18);
    printf("%d \n", value);

    return 0;
}
```
