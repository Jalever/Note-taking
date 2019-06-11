---
layout: post
title: KMP(Knuth-Morris-Pratt) Algorithm
subtitle: Pattern Searching学习笔记系列
date: 2019-06-11
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Algorithm
---

## Overview

## Solution

#### Diagram

#### Implementation in CPP
```cpp
#include <bits/stdc++.h>
using namespace std;

void getLongestProperSuffix(char* str,int length,int* arr) {
	int maxMatchingLength = 0;
	int index = 1;
	arr[0] = 0;

	while(index < length) {
		if(str[index] == str[maxMatchingLength]) {
			maxMatchingLength++;
			arr[index] = maxMatchingLength;
			index++;
		} else {
			if(maxMatchingLength != 0) {
				maxMatchingLength = arr[maxMatchingLength-1];
			} else {
				arr[index] = 0;
				index++;
			}
		}
	}
}

void Search(char* text,char* pattern) {
	int textLength = strlen(text);
	int patternLength = strlen(pattern);

	int arr[patternLength];

	getLongestProperSuffix(pattern, patternLength, arr);

	int textIndex = 0;
	int patternIndex = 0;

	while(textIndex < textLength) {
		if(text[textIndex] == pattern[patternIndex]) {
			textIndex++;
			patternIndex++;
		}

		if(patternIndex == patternLength) {
			cout << "Found pattern at index: " << textIndex-patternIndex << endl;
			patternIndex = arr[patternIndex-1];
		} else if(textIndex < textLength && text[textIndex] != pattern[patternIndex]) {
			if(patternIndex != 0) {
				patternIndex = arr[patternIndex-1];
			} else {
				textIndex = textIndex + 1;
			}
		}
	}
}

void traverseArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        cout << arr[i] << " ";
}

int main() {
	char text[] = "AAAAABAAABA";
	char pattern[] = "AAAA";

	Search(text, pattern);

	return 0;
}
```
