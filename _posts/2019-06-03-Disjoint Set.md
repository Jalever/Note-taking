---
layout: post
title: (DS Graph)Disjoint Set
subtitle: Data Structure Graph Cycle
date: 2019-06-03
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Data Structure
---

A disjoint-set data structure is a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets.

A union-find algorithm is an algorithm that performs two useful operations on such a data structure:

- Find:
Determine which subset a particular element is in. This can be used for determining if two elements are in the same subset.

- Union:
Join two subsets into a single subset.

Union-Find Algorithm can be used to check whether an undirected graph contains cycle or not.


```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>//defines void *memset(void *str, int c, size_t n)

struct Edge {
    int source,
        distance;
};

struct Graph{
    int verticleNum,
        edgeNum;

    struct Edge* edge;
};

struct Graph* createGraph(int verticleNum, int edgeNum) {
    struct Graph* graph = (struct Graph*)malloc( sizeof(struct Graph) );

    graph->verticleNum = verticleNum;
    graph->edgeNum = edgeNum;

    graph->edge = (struct Edge*)malloc((graph->edgeNum) * (sizeof(struct Edge)));

    return graph;
}

int Find(int parent[], int i) {
    if(parent[i] != -1) {
        return -1;
    }

    return Find(parent, parent[i]);
}

void Union(int parent[], int x, int y) {
    int xset = Find(parent, x);
    int yset = Find(parent, y);

    if(xset != yset) {
        parent[xset] = yset;
    }
}

int isCircle(struct Graph* graph) {

    int *parent = (int*)malloc((graph->verticleNum) * (sizeof(int)));
    memset(parent, -1, ( graph->verticleNum) * ( sizeof(int) ) );

    for(int i = 0;i < graph->edgeNum;++i) {
        int x = Find(parent, graph->edge[i].source);
        int y = Find(parent, graph->edge[i].distance);

        if(x == y) {
            return 1;
        } else {
            Union(parent, x, y);
        }
    }

    return 0;
}

int main() {
    int verticleNum = 3;
    int edgeNum = 3;

    struct Graph* graph =  createGraph(verticleNum, edgeNum);

    graph->edge[0].source = 0;
    graph->edge[0].distance = 1;
    graph->edge[1].source = 1;
    graph->edge[1].distance = 2;
    graph->edge[2].source = 2;
    graph->edge[2].distance = 0;

    if(isCircle(graph)) {
		printf( "graph contains cycle" );
    } else {
		printf( "graph doesn't contain cycle" );
    }

    return 0;
}
```
