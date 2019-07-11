---
layout: post
title: Eight Queen Puzzle
subtitle: Backtracking Paradigm
date: 2019-07-03
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---
## Overview
The <strong>Eight Queens Puzzle</strong> is the problem of placing eight chess queens on an `8×8` Chessboard so that no two queens threaten each other; thus, a solution requires that no two queens share the same row, column, or diagonal. The eight queens puzzle is an example of the more general `n` queens problem of placing `n` non-attacking queens on an `n×n` chessboard, for which solutions exist for all natural numbers n with the exception of `n = 2` and `n = 3`.

## History
Chess composer <strong>Max Bezzel</strong> published the Eight Queens Puzzle in 1848. <strong>Franz Nauck</strong> published the first solutions in 1850. <strong>Nauck</strong> also extended the puzzle to the `n` queens problem, with `n` queens on a chessboard of `n×n` squares.

Since then, many mathematicians, including <strong>Carl Friedrich Gauss</strong>, have worked on both the Eight Queens Puzzle and its generalized n-queens version. In 1874, <strong>S. Gunther</strong> proposed a method using determinants to find solutions. <strong>J.W.L. Glaisher</strong> refined <strong>Gunther</strong>'s approach.

In 1972, <strong>Edsger Dijkstra</strong> used this problem to illustrate the power of what he called structured programming. He published a highly detailed description of a Depth-First Backtracking Algorithm.

## Constructing and Counting Solutions
The problem of finding all solutions to the 8-queens problem can be quite computationally expensive, as there are `4,426,165,368` (i.e., 64C8) possible arrangements of eight queens on an `8×8` board, but only 92 solutions. It is possible to use shortcuts that reduce computational requirements or rules of thumb that avoids Brute-Force Computational Techniques. For example, by applying a simple rule that constrains each queen to a single column (or row), though still considered brute force, it is possible to reduce the number of possibilities to `16,777,216` (that is, `8 exponent 8`) possible combinations. Generating permutations further reduces the possibilities to just `40,320` (that is, `8!`), which are then checked for diagonal attacks.

#### Solutions
The <strong>Eight Queens Puzzle</strong> has 92 distinct solutions. If solutions that differ only by the symmetry operations of rotation and reflection of the board are counted as one, the puzzle has 12 solutions. These are called <strong>Fundamental Solutions</strong>;

A <strong>fundamental solution</strong> usually has eight variants (including its original form) obtained by rotating `90°`, `180°`, or `270°` and then reflecting each of the four rotational variants in a mirror in a fixed position. However, should a solution be equivalent to its own 90° rotation (as happens to one solution with five queens on a 5×5 board), that fundamental solution will have only two variants (itself and its reflection). Should a solution be equivalent to its own 180° rotation (but not to its 90° rotation), it will have four variants (itself and its reflection, its 90° rotation and the reflection of that). If `n > 1`, it is not possible for a solution to be equivalent to its own reflection because that would require two queens to be facing each other. Of the 12 fundamental solutions to the problem with eight queens on an `8×8` board, exactly one (solution 12 below) is equal to its own `180°` rotation, and none is equal to its `90°` rotation; thus, the number of distinct solutions is `11×8 + 1×4 = 92`.

All fundamental solutions are presented below:
![Z2QVZ4.png](https://s2.ax1x.com/2019/07/11/Z2QVZ4.png)
![Z2Qeo9.png](https://s2.ax1x.com/2019/07/11/Z2Qeo9.png)
![Z2QlQK.png](https://s2.ax1x.com/2019/07/11/Z2QlQK.png)

`Solution 10` has the additional property that no <strong>Three-Queens-Are-In-A-Straight-Line</strong>.

## Implementation in CPP
```cpp
#include <iostream>
using namespace std;

#define N 8

void printChessboard(int board[N][N]) {
	for (int i = 0; i < N; i++) {
		for (int j = 0; j < N; j++) {
			cout << board[i][j] << " ";
		}

		cout << "\n";
	}
}

bool isValidCoordinate(int board[N][N], int row, int column) {
	int horizontal, vertical;
	for (horizontal = 0; horizontal < column; horizontal++) {
		if (board[row][horizontal]) {
			return false;
		}
	}

	for (vertical = row, horizontal = column; vertical >= 0 && horizontal >= 0; vertical--, horizontal--) {
		if (board[vertical][horizontal]) {
			return false;
		}
	}

	for (vertical = row, horizontal = column; horizontal >= 0 && vertical < N; vertical++, horizontal--){
		if (board[vertical][horizontal]) {
			return false;
		}
	}

	return true;
}

bool NQueenProblemUtil(int Chessboard[N][N], int column) {
	if (column >= N) {
		return true;
	}

	for (int r = 0; r < N; r++) {
		if (isValidCoordinate(Chessboard, r, column)) {
			Chessboard[r][column] = 1;

			if (NQueenProblemUtil(Chessboard, column + 1)) {
				return true;
			}

			Chessboard[r][column] = 0;
		}
	}

	return false;
}

bool NQueenProblem() {
	int Chessboard[N][N] = {
			{ 0, 0, 0, 0, 0, 0, 0, 0 },
			{ 0, 0, 0, 0, 0, 0, 0, 0 },
			{ 0, 0, 0, 0, 0, 0, 0, 0 },
			{ 0, 0, 0, 0, 0, 0, 0, 0 },
			{ 0, 0, 0, 0, 0, 0, 0, 0 },
			{ 0, 0, 0, 0, 0, 0, 0, 0 },
			{ 0, 0, 0, 0, 0, 0, 0, 0 },
			{ 0, 0, 0, 0, 0, 0, 0, 0 }
	};

	if (NQueenProblemUtil(Chessboard, 0) == false) {
		cout << "Solution does not exist." << endl;
		return false;
	}

	printChessboard(Chessboard);
	return true;
}

int main() {
	NQueenProblem();
	return 0;
}

```

#### Output
![Z2rMse.png](https://s2.ax1x.com/2019/07/11/Z2rMse.png)
