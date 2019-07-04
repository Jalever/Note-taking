---
layout: post
title: The Knight Tour Problem
subtitle: Backtracking Paradigm
date: 2019-07-03
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
- [Introduction](#introduction)
- [Solutions](#solutions)
    - [Naive Algorithm for Knight tour](#naive-algorithm-for-knight-tour)
    - [Backtracking Algorithm for Knight tour](#backtracking-algorithm-for-knight-tour)
        - [Implementation in CPP Using Backtracking Algorithm for Knight tour](#implementation-in-cpp-using-backtracking-algorithm-for-knight-tour)

## Introduction
A knight's tour is a sequence of moves of a knight on a chessboard such that the knight visits every square only once.

If the knight ends on a square that is one knight's move from the beginning square (so that it could tour the board again immediately, following the same path), the tour is `closed`, otherwise it is `open`.

The knight's tour problem is the mathematical problem of finding a knight's tour. Creating a program to find a knight's tour is a common problem given to computer science students. Variations of the knight's tour problem involve chessboards of different sizes than the usual `8 × 8`, as well as irregular (non-rectangular) boards.

An open knight's tour of a chessboard
![ZYsQG8.gif](https://s2.ax1x.com/2019/07/03/ZYsQG8.gif)

The moves of a knight are:
![ZYr4Ds.gif](https://s2.ax1x.com/2019/07/03/ZYr4Ds.gif)

## Solutions
#### Naive Algorithm for Knight tour
The Naive Algorithm is to generate all tours one by one and check if the generated tour satisfies the constraints.
```cpp
while there are untried tours
{
   generate the next tour
   if this tour covers all squares
   {
      print this path;
   }
}
```

#### Backtracking Algorithm for Knight tour
Backtracking works in an incremental way to attack problems. Typically, we start from an empty solution vector and one by one add items (Meaning of item varies from problem to problem. In context of Knight’s tour problem, an item is a Knight’s move). When we add an item, we check if adding the current item violates the problem constraint, if it does then we remove the item and try other alternatives. If none of the alternatives work out then we go to previous stage and remove the item added in the previous stage. If we reach the initial stage back then we say that no solution exists. If adding an item doesn’t violate constraints then we recursively add items one by one. If the solution vector becomes complete then we print the solution.

Following is the Backtracking algorithm for Knight’s tour problem.
```
If all squares are visited
    print the solution
Else
   a) Add one of the next moves to solution vector and recursively
   check if this move leads to a solution. (A Knight can make maximum
   eight moves. We choose one of the 8 moves in this step).

   b) If the move chosen in the above step doesn't lead to a solution
   then remove this move from the solution vector and try other
   alternative moves.

   c) If none of the alternatives work then return false (Returning false
   will remove the previously added item in recursion and if false is
   returned by the initial call of recursion then "no solution exists" )
```

###### Implementation in CPP Using Backtracking Algorithm for Knight tour
```cpp
#include <iostream>
#define N 8

using namespace std;

bool isValidCoordinate(int XAxis,int YAxis,int Chessboard[N][N]) {
	return (XAxis >= 0 && YAxis >= 0 && XAxis < N && YAxis < N && Chessboard[XAxis][YAxis] == -1 );
}

void PrintSolution(int Chessboard[N][N]) {
	for(int i = 0;i < N;i++) {
		for(int j = 0;j < N;j++) {
			cout << Chessboard[i][j] << "\t";
		}

		cout << "\n" << endl;
	}
}

bool RecursiveUtilityFunction(int XAxis,int YAxis,int moveSum, int Chessboard[N][N], int XMove[N], int YMove[N]) {
	if(moveSum == N*N) {
		return true;
	}

	cout << "[" << XAxis << "," << YAxis << "]" << endl;

	for(int i = 0;i < N;++i) {
		int NextXAxis = XAxis + XMove[i];
		int NextYAxis = YAxis + YMove[i];

		if(isValidCoordinate(NextXAxis, NextYAxis, Chessboard)) {
			Chessboard[NextXAxis][NextYAxis] = moveSum;

			if(RecursiveUtilityFunction(NextXAxis, NextYAxis, moveSum+1, Chessboard, XMove, YMove) == true) {
				return true;
			} else {
				Chessboard[NextXAxis][NextYAxis] = -1;
			}
		}
	}

	return false;
}

void KnightTour() {
	int Chessboard[N][N];

	for(int i = 0;i < N;++i) {
		for(int j = 0;j < N;++j) {
			Chessboard[i][j] = -1;
		}
	}

	int XNextValidAxis[8] = {2, 1, -1, -2, -2, -1,  1,  2};
	int YNextValidAxis[8] = {1, 2,  2,  1, -1, -2, -2, -1};

	Chessboard[0][0] = 0;

	if(RecursiveUtilityFunction(0, 0, 1, Chessboard, XNextValidAxis, YNextValidAxis)) {
		::PrintSolution(Chessboard);
	} else {
		cout << "Solution doesn't exit!" << endl;
	}
}

int main() {
	::KnightTour();

	return 0;
}
```

output:
![ZY6WvD.png](https://s2.ax1x.com/2019/07/03/ZY6WvD.png)
