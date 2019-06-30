---
layout: post
title: (DS Graph)DFS
subtitle: Data Structure学习笔记系列
date: 2019-05-31
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Data Structure
---

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

    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Following is Depth First Traversal"
            " (starting from vertex 2) \n";
    g.DFS(2);

    return 0;
}
```
