---
layout: post
title: (DS Graph)Depth First Search
subtitle: Data Structure Traverse
date: 2019-05-31
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Data Structure
---

- [Overview](#overview)
- [Implementation of Adajacent List](#implementation-of-adajacent-list)

## Overview
Depth first search (DFS) algorithm starts with the initial node of the graph G, and then goes to deeper and deeper until we find the goal node or the node which has no children. The algorithm, then backtracks from the dead end towards the most recent node that is yet to be completely unexplored.

The data structure which is being used in DFS is stack. The process is similar to BFS algorithm. In DFS, the edges that leads to an unvisited node are called discovery edges while the edges that leads to an already visited node are called block edges.

## Implementation of Adajacent List
![Z1zKRe.png](https://s2.ax1x.com/2019/06/30/Z1zKRe.png)
![Z1z3qI.png](https://s2.ax1x.com/2019/06/30/Z1z3qI.png)
![Z1zJdP.png](https://s2.ax1x.com/2019/06/30/Z1zJdP.png)
![Z1zYIf.png](https://s2.ax1x.com/2019/06/30/Z1zYIf.png)

![eXMCU1.png](https://s2.ax1x.com/2019/08/10/eXMCU1.png)
![eXMFC6.png](https://s2.ax1x.com/2019/08/10/eXMFC6.png)
![eXMAgO.png](https://s2.ax1x.com/2019/08/10/eXMAgO.png)
![eXMZKe.png](https://s2.ax1x.com/2019/08/10/eXMZKe.png)

```cpp
#include <iostream>

#include <list>

using namespace std;

class Graph {
    int vectorSum;
    list<int> *adjacentArr;
    void DFSUtil(int currentNode, bool visited[]);

    public:
        Graph(int vectorSum);
        void addEdge(int node, int weight);
        void DFS(int vector);
};

Graph::Graph(int vectorSum) {
    this -> vectorSum = vectorSum;
    adjacentArr = new list<int>[vectorSum];
}

void Graph::addEdge(int node, int weight) {
    adjacentArr[node].push_back(weight);
};

void Graph::DFSUtil(int currentNode,bool visited[]) {
    visited[currentNode] = true;

    cout << currentNode << " ";

    list<int>::iterator i;

    for(i = adjacentArr[currentNode].begin();i != adjacentArr[currentNode].end();++i) {
        if(!visited[*i]) {
            DFSUtil(*i, visited);
        }
    }
}

void Graph::DFS(int currentNode) {
    bool *visited = new bool[vectorSum];

    for(int i = 0;i < vectorSum;++i) {
        visited[i] = false;
    }


    DFSUtil(currentNode, visited);
}

int main() {

    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(0, 3);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 4);
    g.addEdge(3, 4);

    cout << "Following is Depth First Traversal"
            " (starting from vertex 2) \n";
    g.DFS(0);

    return 0;
}
```
