---
layout: post
title: (DS Graph)Prim Shortest Path Algorithm
subtitle: Data Structure Graph学习笔记系列
date: 2019-06-08
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Data Structure
---

- [Spanning Tree](#spanning-tree)
- [Minimum Spanning Tree](#minimum-spanning-tree)
- [Prim Algorithm](#prim-algorithm)
- [Example](#example)
    - [Steps](#steps)
- [Implementation in CPP](#implementation-in-cpp)

## Spanning Tree
Spanning tree can be defined as a sub-graph of connected, undirected graph G that is a tree produced by removing the desired number of edges from a graph. In other words, Spanning tree is a <ins>non-cyclic sub-graph of a connected and undirected graph G that connects all the vertices together</ins>. A graph G can have multiple spanning trees.

## Minimum Spanning Tree
There can be weights assigned to every edge in a weighted graph. However, A minimum spanning tree is a spanning tree which has <ins>minimal total weight</ins>. In other words, minimum spanning tree is the one which contains the least weight among all other spanning tree of some particular graph.

## Prim Algorithm
Prim's Algorithm is used to find the minimum spanning tree from a graph. Prim's algorithm finds the subset of edges that includes every vertex of the graph such that the sum of the weights of the edges can be minimized.

Prim's algorithm starts with the single node and explore all the adjacent nodes with all the connecting edges at every step. The edges with the minimal weights causing no cycles in the graph got selected.

## Example
Construct a minimum spanning tree of the graph given in the following figure by using prim's algorithm.

![Z3VSg0.png](https://s2.ax1x.com/2019/06/30/Z3VSg0.png)

#### Steps
1. Choose a starting vertex B.
2. Add the vertices that are adjacent to A. the edges that connecting the vertices are shown by dotted lines.
3. Choose the edge with the minimum weight among all. i.e. BD and add it to MST. Add the adjacent vertices of D i.e. C and E.
4. Choose the edge with the minimum weight among all. In this case, the edges DE and CD are such edges. Add them to MST and explore the adjacent of C i.e. E and A.
5. Choose the edge with the minimum weight i.e. CA. We can't choose CE as it would cause cycle in the graph.

```text
B -> BD -> BD, DE -> BD, DE, DC -> BD, DE, DC, CA
```

The graph produces in the step 5 is the minimum spanning tree of the graph shown in the above figure.

The cost of MST will be calculated as;

cost(MST) = 4 + 2 + 1 + 3 = 10 units.

![Z3VaKf.png](https://s2.ax1x.com/2019/06/30/Z3VaKf.png)

## Implementation in CPP

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
