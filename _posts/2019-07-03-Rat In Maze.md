---
layout: post
title: Rat in Maze
subtitle: Backtracking学习笔记系列
date: 2019-07-03
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

- [Introduction](#introduction)
    - [Illustration](#illustration)
- [Solutions](#solutions)
    - [Naive Algorithm](#naive-algorithm)
    - [Backtracking Algorithm](#backtracking-algorithm)
        - [Implementation using Backtracking Algorithm in CPP](#implementation-using-backtracking-algorithm-in-cpp)

## Introduction
A Maze is given as `N*N` binary matrix of blocks where <ins>source block</ins> is <ins>the upper leftmost block</ins> i.e., maze[0][0] and <ins>destination block</ins> is <ins>lower rightmost block</ins> i.e., maze[N-1][N-1]. A rat starts from source and has to reach the destination. The rat can move only in two directions: <ins><strong>forward</strong></ins> and <ins><strong>down</strong></ins>.
In the maze matrix, <ins>0</ins> means the block is a <ins><strong>dead end</strong></ins> and <ins>1</ins> means <ins><strong>the block can be used in the path from source to destination</strong></ins>.

#### Illustration
Following is an example maze.

```
Gray blocks are dead ends (value = 0).
```

![ZYWCmF.png](https://s2.ax1x.com/2019/07/03/ZYWCmF.png)

Following is binary matrix representation of the above maze.

```
{1, 0, 0, 0}
{1, 1, 0, 1}
{0, 1, 0, 0}
{1, 1, 1, 1}
```

Following is a maze with highlighted solution path.

![ZYWnOO.png](https://s2.ax1x.com/2019/07/03/ZYWnOO.png)

Following is the solution matrix (output of program) for the above input matrx.

```text
                {1, 0, 0, 0}
                {1, 1, 0, 0}
                {0, 1, 0, 0}
                {0, 1, 1, 1}
 All enteries in solution path are marked as 1.
```

## Solutions

#### Naive Algorithm
The Naive Algorithm is to generate all paths from source to destination and one by one check if the generated path satisfies the constraints.

```text
while there are untried paths
{
   generate the next path
   if this path has all blocks as 1
   {
      print this path;
   }
}
```

#### Backtracking Algorithm
```text
If destination is reached
    print the solution matrix
Else
   a) Mark current cell in solution matrix as 1.
   b) Move forward in the horizontal direction and recursively check if this
       move leads to a solution.
   c) If the move chosen in the above step doesn't lead to a solution
       then move down and check if this move leads to a solution.
   d) If none of the above solutions works then unmark this cell as 0
       (BACKTRACK) and return false.
```

###### Implementation using Backtracking Algorithm in CPP
```cpp
#include <iostream>
#define N 4

using namespace std;

void PrintSolutionMatrix(int SolutionMatrix[N][N]) {
	for(int i = 0;i < N;i++) {
		for(int j = 0;j < N;j++) {
			cout << SolutionMatrix[i][j] << " ";
		}

		cout << "\n";
	}
}

bool isValidCoordinate(int Maze[N][N],int XAxis,int YAxis) {
	if(XAxis >= 0 && YAxis >= 0 && XAxis < N && YAxis < N && Maze[XAxis][YAxis] == 1) {
		return true;
	}

	return false;
}

bool RecursiveUtilityFunction(int Maze[N][N],int XAxis,int YAxis,int SolutionMatrix[N][N]) {
	if(XAxis == N-1 && YAxis == N-1) {
		SolutionMatrix[XAxis][YAxis] = 1;
		return true;
	}

	if(::isValidCoordinate(Maze, XAxis, YAxis)) {
		SolutionMatrix[XAxis][YAxis] = 1;

		if(::RecursiveUtilityFunction(Maze, XAxis+1, YAxis, SolutionMatrix)) {
			return true;
		}

		if(::RecursiveUtilityFunction(Maze, XAxis, YAxis+1, SolutionMatrix)) {
			return true;
		}

		SolutionMatrix[XAxis][YAxis] = 0;
		return false;
	}

	return false;
}

void RatInMaze(int Maze[N][N]) {
	int SolutionMatrix[N][N] = {
			{0, 0, 0, 0},
			{0, 0, 0, 0},
			{0, 0, 0, 0},
			{0, 0, 0, 0}
	};

	if(::RecursiveUtilityFunction(Maze, 0, 0, SolutionMatrix)) {
		::PrintSolutionMatrix(SolutionMatrix);
	} else {
		cout << "Solution path doesn't exist!" << endl;
	}
}



int main() {
	int Maze[N][N] = {
			{1, 0, 0, 0},
			{1, 1, 0, 1},
			{0, 1, 0, 0},
			{1, 1, 1, 1}
	};

	::RatInMaze(Maze);

	return 0;
}
```
