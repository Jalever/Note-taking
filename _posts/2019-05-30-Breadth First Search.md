---
layout: post
title: (DS Graph)BFS
subtitle: Data Structure学习笔记系列
date: 2019-05-30
author: Jalever
header-img: img/post-bg-star.jpg
catalog: true
tags:
  - Data Structure
---

## Implementation of Adajacent List

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
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Following is Breadth First Traversal "
         << "(starting from vertex 2) \n";
    g.BFS(2);

    return 0;
}
```

## Time Complexity
`O(V+E)` where `V` is number of vertices in the graph and `E` is number of edges in the graph.
