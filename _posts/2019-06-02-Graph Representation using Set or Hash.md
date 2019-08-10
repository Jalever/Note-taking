---
layout: post
title: (DS Graph)Graph Representation using Set or Hash
subtitle: Data Structure Graph
date: 2019-06-02
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Data Structure
---

## Adjacency List Representation of an Undirected Graph using Sets:
```cpp
#include<bits/stdc++.h>

using namespace std;

struct Graph{
    int vectorSum;
    set<int ,greater<int> >* adjacentList;
};

Graph* createGraph(int vectorSum) {
    Graph* graph = new Graph;
    graph -> vectorSum = vectorSum;
    graph -> adjacentList = new set<int, greater<int> >[vectorSum];

    return graph;
}

void addEdge(Graph* graph, int source, int destination) {
    graph->adjacentList[source].insert(destination);
    graph->adjacentList[destination].insert(source);
}

void printGraph(Graph* graph) {
    for(int i = 0;i < graph->vectorSum;++i) {
        set<int, greater<int>> queue = graph->adjacentList[i];

        cout << endl << "Adjacent List of Vertex: " << i << endl;

        for(auto iterator = queue.begin();iterator != queue.end();++iterator) {
            cout << *iterator << " ";
        }

    }
}

void searchEdge(Graph* graph,int source,int destination) {

    auto iterator = graph->adjacentList[source].find(destination);

    if(iterator == graph->adjacentList[source].end()) {
        cout << endl << "Edge from " << source << " to " << destination << " not found";
    } else {
        cout << endl << "Edge from " << source << " to " << destination << " were found";

    }
}

int main() {
    struct Graph *graph = createGraph(5);

    addEdge(graph, 0, 1);
    addEdge(graph, 0, 4);
    addEdge(graph, 1, 2);
    addEdge(graph, 1, 3);
    addEdge(graph, 1, 4);
    addEdge(graph, 2, 3);
    addEdge(graph, 3, 4);

    // Print the adjacency list representation of

    // the above graph

    printGraph(graph);

    searchEdge(graph, 0, 3);

    return 0;
}
```
- Pros:
Queries like whether there is an edge from vertex u to vertex v can be done in `O(log V)`.

- Cons:
Adding an edge takes `O(log V)`, as opposed to O(1) in vector implementation.<br/>
Graphs containing parallel edge(s) cannot be implemented through this method.


## Optimization of Edge Search Operation using unordered_set (or hashing)
```cpp
#include <bits/stdc++.h>

using namespace std;

struct Graph {
    int V;
    unordered_set<int>* adjList;
};

// A utility function that creates a graph of  

// V vertices

Graph* createGraph(int V)
{
    Graph* graph = new Graph;
    graph->V = V;

    // Create an array of sets representing

    // adjacency lists. Size of the array will be V

    graph->adjList = new unordered_set<int>[V];

    return graph;
}

// Adds an edge to an undirected graph

void addEdge(Graph* graph, int src, int dest)
{
    // Add an edge from src to dest. A new

    // element is inserted to the adjacent

    // list of src.

    graph->adjList[src].insert(dest);

    // Since graph is undirected, add an edge

    // from dest to src also

    graph->adjList[dest].insert(src);
}

// A utility function to print the adjacency

// list representation of graph

void printGraph(Graph* graph)
{
    for (int i = 0; i < graph->V; ++i) {
        unordered_set<int> lst = graph->adjList[i];
        cout << endl << "Adjacency list of vertex "
             << i << endl;

        for (auto itr = lst.begin(); itr != lst.end(); ++itr)
            cout << *itr << " ";
        cout << endl;
    }
}

// Searches for a given edge in the graph

void searchEdge(Graph* graph, int src, int dest)
{
    auto itr = graph->adjList[src].find(dest);
    if (itr == graph->adjList[src].end())
        cout << endl << "Edge from " << src
             << " to " << dest << " not found."
             << endl;
    else
        cout << endl << "Edge from " << src
             << " to " << dest << " found."
             << endl;
}

// Driver code

int main()
{
    // Create the graph given in the above figure

    int V = 5;
    struct Graph* graph = createGraph(V);
    addEdge(graph, 0, 1);
    addEdge(graph, 0, 4);
    addEdge(graph, 1, 2);
    addEdge(graph, 1, 3);
    addEdge(graph, 1, 4);
    addEdge(graph, 2, 3);
    addEdge(graph, 3, 4);

    // Print the adjacency list representation of

    // the above graph

    printGraph(graph);

    // Search the given edge in the graph

    searchEdge(graph, 2, 1);
    searchEdge(graph, 0, 3);

    return 0;
}
```

- Pros:
1. Queries like whether there is an edge from vertex u to vertex v can be done in `O(1)`.
2. Adding an edge takes `O(1)`.

- Cons:
1. Graphs containing parallel edge(s) cannot be implemented through this method.
2. Edges are not stored in any order.
