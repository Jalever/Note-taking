---
layout: post
title: (DS Graph)Graph Overview
subtitle: Data Structure Graph学习笔记系列
date: 2019-05-29
author: Jalever
header-img: img/post-bg-star.jpg
catalog: true
tags:
  - Data Structure
---
- [Overview](#overview)
- [Directed and Undirected Graph](#directed-and-undirected-graph)
    - [Undirected Graph](#undirected-graph)
    - [Directed Graph](#directed-graph)
- [Terminology](#terminology)
    - [Path](#path)
    - [Closed Path](#closed-path)
    - [Simple Path](#simple-path)
    - [Cycle](#cycle)
    - [Connected Graph](#connected-graph)
    - [Complete Graph](#complete-graph)
    - [Weighted Graph](#weighted-graph)
    - [Digraph](#digraph)
    - [Loop](#loop)
    - [Adjacent Nodes](#adjacent-nodes)
    - [Degree of the Node](#degree-of-the-node)
- [Graph Representation](#graph-representation)
    - [Sequential Representation](#sequential-representation)
        - [Undirected Graph and Adjacency Matrix](#undirected-graph-and-adjacency-matrix)
        - [Directed Graph and Adjacency Matrix](#directed-graph-and-adjacency-matrix)
        - [Weighted Directed Graph and Adjacency Matrix](#weighted-directed-graph-and-adjacency-matrix)
    - [Linked Representation](#linked-representation)
        - [Undirected Graph and Adjacency List](#undirected-graph-and-adjacency-list)
        - [Directed Graph and Adjacency List](#directed-graph-and-adjacency-list)
        - [Weighted Directed Graph and Adjacency List](#weighted-directed-graph-and-adjacency-list)
- [Operations](#operations)
    - [Traversal](#traversal)
        - [BFS](#bfs)
        - [DFS](#dfs)
    - [Minimum Spanning Tree](#minimum-spanning-tree)
        - [Prim](#prim)
        - [Kruskal](#kruskal)
    - [Shortest Path First Algorithm](#shortest-path-first-algorithm)
        - [Dijkstra](#dijkstra)
        - [Floyd-Washall Algorithm](#floyd-washall-algorithm)
    - [Sorting](#sorting)
        - [Topological Sorting](#topological-sorting)


## Overview
A graph can be defined as group of vertices and edges that are used to connect these vertices. A graph can be seen as a cyclic tree, where the vertices (Nodes) maintain any complex relationship among them instead of having parent child relationship.

A graph `G` can be defined as an ordered set `G(V, E)` where `V(G)` represents the set of vertices and `E(G)` represents the set of edges which are used to connect these vertices.

A Graph `G(V, E)` with 5 vertices `(A, B, C, D, E)` and six edges `((A,B), (B,C), (C,E), (E,D), (D,B), (D,A))` is shown in the following figure.

![Z18vDA.png](https://s2.ax1x.com/2019/06/30/Z18vDA.png)

## Directed and Undirected Graph
A graph can be directed or undirected.

#### Undirected Graph
In an undirected graph, edges are not associated with the directions with them. An undirected graph is shown in the above figure since its edges are not attached with any of the directions. If an edge exists between vertex `A` and `B` then the vertices can be traversed from `B` to `A` as well as `A` to `B`.

#### Directed Graph
In a directed graph, edges form an ordered pair. Edges represent a specific path from some vertex A to another vertex B. Node A is called initial node while node B is called terminal node.

A directed graph is shown in the following figure.
![Z1GPC8.png](https://s2.ax1x.com/2019/06/30/Z1GPC8.png)

## Terminology

#### Path
A path can be defined as the sequence of nodes that are followed in order to reach some terminal node V from the initial node U.

#### Closed Path
A path will be called as closed path if the initial node is same as terminal node. A path will be closed path if `V0=VN`.

#### Simple Path
If all the nodes of the graph are distinct with an exception `V0=VN`, then such path `P` is called as `Closed Simple Path`.

#### Cycle
A cycle can be defined as the path which has no repeated edges or vertices except the first and last vertices.

#### Connected Graph
A connected graph is the one in which some path exists between every two vertices (u, v) in V. There are no isolated nodes in connected graph.

#### Complete Graph
A complete graph is the one in which every node is connected with all other nodes. A complete graph contain `n(n-1)/2` edges where `n` is the number of nodes in the graph.

#### Weighted Graph
In a weighted graph, each edge is assigned with some data such as length or weight. The weight of an edge e can be given as `w(e)` which must be a positive `(+)` value indicating the cost of traversing the edge.

#### Digraph
A digraph is a directed graph in which each edge of the graph is associated with some direction and the traversing can be done only in the specified direction.

#### Loop
An edge that is associated with the similar end points can be called as Loop.

#### Adjacent Nodes
If two nodes u and v are connected via an edge e, then the nodes u and v are called as neighbours or adjacent nodes.

#### Degree of the Node
A degree of a node is the number of edges that are connected with that node. A node with degree 0 is called as isolated node.

## Graph Representation

#### Sequential Representation
In sequential representation, we use adjacency matrix to store the mapping represented by vertices and edges. In adjacency matrix, the rows and columns are represented by the graph vertices. A graph having n vertices, will have a dimension n x n.

###### Undirected Graph and Adjacency Matrix
An entry `Mij` in the adjacency matrix representation of an undirected graph `G` will be 1 if there exists an edge between `Vi` and `Vj`.

An undirected graph and its adjacency matrix representation is shown in the following figure.

![Z1tVDH.png](https://s2.ax1x.com/2019/06/30/Z1tVDH.png)

in the above figure, we can see the mapping among the vertices (A, B, C, D, E) is represented by using the adjacency matrix which is also shown in the figure.

###### Directed Graph and Adjacency Matrix
In directed graph, an entry `Aij` will be 1 only when there is an edge directed from `Vi` to `Vj`.

A directed graph and its adjacency matrix representation is shown in the following figure.

![Z1tBxU.png](https://s2.ax1x.com/2019/06/30/Z1tBxU.png)

###### Weighted Directed Graph and Adjacency Matrix
Representation of weighted directed graph is different. Instead of filling the entry by 1, the Non- zero entries of the adjacency matrix are represented by the weight of respective edges.

The weighted directed graph along with the adjacency matrix representation is shown in the following figure.

![Z1tsr4.png](https://s2.ax1x.com/2019/06/30/Z1tsr4.png)

#### Linked Representation
In the linked representation, an adjacency list is used to store the Graph into the computer's memory.

###### Undirected Graph and Adjacency List
Consider the undirected graph shown in the following figure and check the adjacency list representation.

![Z1tjRf.png](https://s2.ax1x.com/2019/06/30/Z1tjRf.png)

An adjacency list is maintained for each node present in the graph which stores the node value and a pointer to the next adjacent node to the respective node. If all the adjacent nodes are traversed then store the NULL in the pointer field of last node of the list. The sum of the lengths of adjacency lists is equal to the twice of the number of edges present in an undirected graph.

###### Directed Graph and Adjacency List
Consider the directed graph shown in the following figure and check the adjacency list representation of the graph.

![Z1NAJ0.png](https://s2.ax1x.com/2019/06/30/Z1NAJ0.png)

In a directed graph, the sum of lengths of all the adjacency lists is equal to the number of edges present in the graph.

###### Weighted Directed Graph and Adjacency List
In the case of weighted directed graph, each node contains an extra field that is called the weight of the node. The adjacency list representation of a directed graph is shown in the following figure.

![Z1NVzT.png](https://s2.ax1x.com/2019/06/30/Z1NVzT.png)

## Operations
#### Traversal
###### BFS
###### DFS

#### Minimum Spanning Tree
###### Prim
###### Kruskal

#### Shortest Path First Algorithm
###### Dijkstra
###### Floyd-Washall Algorithm

#### Sorting
###### Topological Sorting
