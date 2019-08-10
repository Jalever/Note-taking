---
layout: post
title: (DS Graph)Breadth First Search
subtitle: Data Structure Traverse
date: 2019-05-30
author: Jalever
header-img: img/post-bg-star.jpg
catalog: true
tags:
  - Data Structure
---

- [Overview](#overview)
- [Implementation of Adajacent List](#implementation-of-adajacent-list)

## Overview
Breadth first search is a graph traversal algorithm that starts traversing the graph from root node and explores all the neighbouring nodes. Then, <ins>it selects the nearest node and explore all the unexplored nodes.</ins> The algorithm follows the same process for each of the nearest node until it finds the goal.

The algorithm of breadth first search is given below. The algorithm starts with examining the node A and all of its neighbours. In the next step, the neighbours of the nearest node of A are explored and process continues in the further steps. The algorithm explores all neighbours of all the nodes and ensures that each node is visited exactly once and no node is visited twice.

## Implementation of Adajacent List
![Z1xdD1.png](https://s2.ax1x.com/2019/06/30/Z1xdD1.png)
![Z1xBE6.png](https://s2.ax1x.com/2019/06/30/Z1xBE6.png)
![Z1xDUK.png](https://s2.ax1x.com/2019/06/30/Z1xDUK.png)
![Z1xyCD.png](https://s2.ax1x.com/2019/06/30/Z1xyCD.png)

![eXmrBn.png](https://s2.ax1x.com/2019/08/10/eXmrBn.png)
![eXm7Ax.png](https://s2.ax1x.com/2019/08/10/eXm7Ax.png)
![eXmO3D.png](https://s2.ax1x.com/2019/08/10/eXmO3D.png)
![eXmXge.png](https://s2.ax1x.com/2019/08/10/eXmXge.png)
```cpp
#include <iostream>

#include <list>

using namespace std;

class Graph {
    int vectorSum;
    list<int> *adjacentArr;
    public:
        Graph(int vectorSum);
        void addEdge(int head, int vector);
        void BFS(int source);
};

Graph::Graph(int vectorSum) {
    this -> vectorSum = vectorSum;
    adjacentArr = new list<int>[vectorSum];
};

void Graph::addEdge(int head, int vector) {
    adjacentArr[head].push_back(vector);
};

void Graph::BFS(int sourceVector) {
    bool *visited = new bool[vectorSum];
    for(int i = 0;i < vectorSum;++i) {
        visited[i] = false;
    }

    list<int> queue;
    visited[sourceVector] = true;
    queue.push_back(sourceVector);

    list<int>::iterator i;

    while(!queue.empty()) {
        int v = queue.front();
        cout << v << " ";
        queue.pop_front();

        for(i = adjacentArr[v].begin();i != adjacentArr[v].end(); ++i) {
            if(!visited[*i]) {
                visited[*i] = true;
                queue.push_back(*i);
            }
        }
    }
};

int main() {
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(0, 3);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 4);
    g.addEdge(3, 4);

    cout << "Following is Breadth First Traversal "
         << "(starting from vertex 2) \n";
    g.BFS(0);

    return 0;
}
```

## Time Complexity
`O(V+E)` where `V` is number of vertices in the graph and `E` is number of edges in the graph.
