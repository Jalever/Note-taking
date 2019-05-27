---
layout: post
title: Prime Number
subtitle: Algorithm学习笔记系列
date: 2019-05-26
author: Jalever
header-img: img/post_2019_react_contextAPI_bg.png
catalog: true
tags:
  - Algorithm
---



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
