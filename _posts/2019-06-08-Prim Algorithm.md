---
layout: post
title: Prim Algorithm
subtitle: Graph学习笔记系列
date: 2019-06-08
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

Prim’s algorithm is a Greedy algorithm.

It starts with an empty spanning tree.

The idea is to maintain two sets of vertices.

The first set contains the vertices already included in the MST, the other set contains the vertices not yet included.

At every step, it considers all the edges that connect the two sets, and picks the minimum weight edge from these edges. After picking the edge, it moves the other endpoint of the edge to the set containing MST.

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include<bits/stdc++.h>

# define VERTICLESUM 5

int getMinIndex(int minWeight[], bool isIncludeInMST[]) {
    int min = INT_MAX,
        minIndex;

    for(int i = 0;i < VERTICLESUM;++i) {
        if(minWeight[i] < min && isIncludeInMST[i] == false) {
            min = minWeight[i];
            minIndex = i;
        }
    }

    return minIndex;
}

void printMST(int edgeHeadArr[],int graph[VERTICLESUM][VERTICLESUM]) {
    printf("Edge:\t Weight\n");

    for(int i = 1;i < VERTICLESUM;++i) {
        printf("%d - %d \t%d \n", edgeHeadArr[i], i, graph[edgeHeadArr[i]][i]);
    }
}

void Prim(int graph[VERTICLESUM][VERTICLESUM]) {
    int priorIndexArr[VERTICLESUM];
    int minWeight[VERTICLESUM];
    bool isIncludedInMST[VERTICLESUM];

    for (int i = 0; i < VERTICLESUM; i++) {
        minWeight[i] = INT_MAX;
        isIncludedInMST[i] = false;
    }

    minWeight[0] = 0;
    priorIndexArr[0] = -1;

    for (int count = 0; count < VERTICLESUM - 1; count++) {
        int row = getMinIndex(minWeight, isIncludedInMST);

        isIncludedInMST[row] = true;

        for (int column = 0; column < VERTICLESUM; column++){

            if (graph[row][column] &&
                isIncludedInMST[column] == false &&
                graph[row][column] < minWeight[column]
            ){
                priorIndexArr[column] = row;
                minWeight[column] = graph[row][column];
            }

        }
    }

    printMST(priorIndexArr, graph);
}


int main() {
    int graph[VERTICLESUM][VERTICLESUM] = {
        { 0, 2, 0, 6, 0 },
        { 2, 0, 3, 8, 5 },
        { 0, 3, 0, 0, 7 },
        { 6, 8, 0, 0, 9 },
        { 0, 5, 7, 9, 0 }
    };

    Prim(graph);

    return 0;
}
```
