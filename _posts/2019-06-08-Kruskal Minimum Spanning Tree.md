---
layout: post
title: Kruskal MST
subtitle: Algorithm学习笔记系列
date: 2019-06-08
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
## What is Minimum Spanning Tree?
Given a connected and undirected graph, a spanning tree of that graph is a subgraph that is a tree and connects all the vertices together.

A minimum spanning tree (MST) or minimum weight spanning tree for a weighted, connected and undirected graph is a spanning tree with weight less than or equal to the weight of every other spanning tree.

The weight of a spanning tree is the sum of weights given to each edge of the spanning tree.

## Time Complexity
O(ElogE) or O(ElogV)

## Source Codes

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Edge {
    int source,
        destination,
        weight;
};

struct Graph {
    int verticleNum,
        edgeNum;

    struct Edge* edge;
};

struct Graph* createGraph(int V, int E) {
    struct Graph* graph = new Graph;
    graph->verticleNum = V;
    graph->edgeNum = E;

    graph->edge = new Edge[E];

    return graph;
}

struct Subset {
    int parent;
    int rank;
};

int Find(struct Subset set[],int i) {
    if(set[i].parent != i) {
        set[i].parent = Find(set, set[i].parent);
    }

    return set[i].parent;
}

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

int isBigger(const void* a, const void* b) {
    struct Edge* a1 = (struct Edge*)a;
    struct Edge* b1 = (struct Edge*)b;

    //true:return 1 , false: return 0
    return a1->weight > b1->weight;
}

void KruskalMST(struct Graph* graph) {
    int verticleNum = graph->verticleNum;

    struct Edge EdgeArray[verticleNum];

    qsort(graph->edge, graph->edgeNum, sizeof(graph->edge[0]), isBigger);

    struct Subset* subsets = (struct Subset*)malloc(verticleNum * sizeof(struct Subset));

    for(int i = 0;i < verticleNum;++i) {
        subsets[i].parent = i;
        subsets[i].rank = 0;
    }

    int v = 0;
    int j = 0;
    while(v < verticleNum-1) {
        struct Edge next_edge = graph->edge[j++];

        int x = Find(subsets, next_edge.source);
        int y = Find(subsets, next_edge.destination);

        if(x != y) {
            EdgeArray[v++] = next_edge;
            Union(subsets, x, y);
        }
    }

    printf("Following are the edges in the constructed MST\n");

    for (int i = 0; i < verticleNum-1; ++i) {

        printf("%d -- %d == %d\n", EdgeArray[i].source, EdgeArray[i].destination, EdgeArray[i].weight);
    }
}



int main()
{
    /* Let us create following weighted graph
             10
        0--------1
        |  \     |
       6|   5\   |15
        |      \ |
        2--------3
            4       */
    int V = 4;  // Number of vertices in graph
    int E = 5;  // Number of edges in graph
    struct Graph* graph = createGraph(V, E);


    // add edge 0-1
    graph->edge[0].source = 0;
    graph->edge[0].destination = 1;
    graph->edge[0].weight = 10;

    // add edge 0-2
    graph->edge[1].source = 0;
    graph->edge[1].destination = 2;
    graph->edge[1].weight = 6;

    // add edge 0-3
    graph->edge[2].source = 0;
    graph->edge[2].destination = 3;
    graph->edge[2].weight = 5;

    // add edge 1-3
    graph->edge[3].source = 1;
    graph->edge[3].destination = 3;
    graph->edge[3].weight = 15;

    // add edge 2-3
    graph->edge[4].source = 2;
    graph->edge[4].destination = 3;
    graph->edge[4].weight = 4;

    KruskalMST(graph);

    return 0;
}
```
