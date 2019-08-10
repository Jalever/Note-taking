---
layout: post
title: (DS Graph)Union-Find Algorithm
subtitle: Data Structure Graph Cycle
date: 2019-06-03
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Data Structure
---

## Optimization
#### Union by Rank  
The idea is to always attach smaller depth tree under the root of the deeper tree.

#### Path Compression
The idea is to flatten the tree when find() is called. When find() is called for an element x, root of the tree is returned. The find() operation traverses up from x to find root. The idea of path compression is to make the found root as parent of x so that we don’t have to traverse all intermediate nodes again.

## Source Codes
```c
#include<stdio.h>
#include<stdlib.h>

struct Edge{
    int source,
        distance;
};

struct Graph{
    int verticleNumber,
        edgeNumber;

    struct Edge* edge;
};

struct Subset{
    int parent,
        rank;
};

struct Graph* createGraph(int verticleNumber, int edgeNumber) {
    struct Graph* graph = (struct Graph*)malloc( sizeof(struct Graph) );

    graph->verticleNumber = verticleNumber;
    graph->edgeNumber = edgeNumber;

    graph->edge = (struct Edge*)malloc((graph->edgeNumber) * sizeof(struct Edge));

    return graph;
};

int Find(struct Subset set[], int i) {
    if(set[i].parent != i) {
        set[i].parent = Find(set, set[i].parent);
    }

    return set[i].parent;
};

void Union(struct Subset set[],int x,int y) {
    int xroot = Find(set, x);
    int yroot = Find(set, y);

    if(set[xroot].rank > set[yroot].rank) {
        set[yroot].parent = xroot;
    } else if(set[xroot].rank < set[yroot].rank) {
        set[xroot].parent = yroot;
    } else {
        set[yroot].parent = xroot;
        set[xroot].rank++;
    }
}

int isCircle(struct Graph* graph) {
    int verticleNumber = graph->verticleNumber;
    int edgeNumber = graph->edgeNumber;

    struct Subset* set = (struct Subset*)malloc(verticleNumber * sizeof(struct Subset));

    for(int i = 0;i < verticleNumber;++i) {
        set[i].parent = i;
        set[i].rank = 0;
    }

    for(int i = 0;i < edgeNumber;++i) {
        int x = Find(set, graph->edge[i].source);
        int y = Find(set, graph->edge[i].distance);

        if(x == y) {
            return 1;
        } else {
            Union(set, x, y);
        }
    }

    return 0;
};

int main() {
    int verticleNumber = 3;
    int edgeNumber = 3;

    struct Graph* graph =  createGraph(verticleNumber, edgeNumber);

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

## Links
[Union By Rank and Path Compression](#https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)
