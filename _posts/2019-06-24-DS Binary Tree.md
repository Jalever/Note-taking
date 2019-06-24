---
layout: post
title: (DS Tree)Binary Tree
subtitle: Data Structure Tree学习笔记系列
date: 2019-06-24
author: Jalever
header-img: img/post-bg-star.jpg
catalog: true
tags:
  - Data Structure
---

- [Introduction](#introduction)
- [Types of Binary Tree](#types-of-binary-tree)
    - [Strictly Binary Tree](#strictly-binary-tree)
    - [Complete Binary Tree](#complete-binary-tree)
- [Binary Tree Traversal](#binary-tree-traversal)
    - [Depth First Traversals](#depth-first-traversals)
        - [Preorder traversal](#preorder-traversal)
        - [Inorder traversal](#inorder-traversal)
        - [Postorder traversal](#postorder-traversal)
        - [Implementation of CPP](#implementation-of-cpp)
    - [Breadth First Traversal](#breadth-first-traversal)
        - [Implementation of Level Order Traversal in CPP](#implementation-of-level-order-Traversal-in-cpp)
- [Binary Tree representation](#binary-tree-traversal)
    - [Linked Representation](#linked-representation)
    - [Sequential Representation](#sequential-representation)

## Introduction
Binary Tree is a special type of generic tree in which, each node can have at most two children. Binary tree is generally partitioned into three disjoint subsets.

1. Root of the node
2. left sub-tree which is also a binary tree.
3. Right binary sub-tree

A binary Tree is shown in the following image.

![ZkLDeK.png](https://s2.ax1x.com/2019/06/24/ZkLDeK.png)

## Types of Binary Tree

#### Strictly Binary Tree
In Strictly Binary Tree, every non-leaf node contain non-empty left and right sub-trees. In other words, <ins>the degree of every non-leaf node will always be 2.</ins> A strictly binary tree with n leaves, will have (2n - 1) nodes.

A strictly binary tree is shown in the following figure.

![ZkLWQI.png](https://s2.ax1x.com/2019/06/24/ZkLWQI.png)

#### Complete Binary Tree
A Binary Tree is said to be a complete binary tree if all of the leaves are located at the same level d. A complete binary tree is a binary tree that contains exactly 2^d nodes at each level between level 0 and d. The total number of nodes in a complete binary tree with depth d is 2^(d+1)-1 where <strong>leaf nodes are 2d</strong> while <strong>non-leaf nodes are 2d-1</strong>.

![ZkOCY4.png](https://s2.ax1x.com/2019/06/24/ZkOCY4.png)

## Binary Tree Traversal
Unlike linear data structures (Array, Linked List, Queues, Stacks, etc) which have only one logical way to traverse them, trees can be traversed in different ways. Following are the generally used ways for traversing trees.

![ZAnw6I.gif](https://s2.ax1x.com/2019/06/24/ZAnw6I.gif)

#### Depth First Traversals
(a) Inorder (Left, Root, Right) : 4 2 5 1 3
(b) Preorder (Root, Left, Right) : 1 2 4 5 3
(c) Postorder (Left, Right, Root) : 4 5 2 3 1

###### Preorder traversal
Traverse the root first then traverse into the left sub-tree and right sub-tree respectively. This procedure will be applied to each sub-tree of the tree recursively.

- Visit the root node
- traverse the left sub-tree in pre-order
- traverse the right sub-tree in pre-order

###### Inorder traversal
Traverse the left sub-tree first, and then traverse the root and the right sub-tree respectively. This procedure will be applied to each sub-tree of the tree recursively.

- Traverse the left sub-tree in in-order
- Visit the root
- Traverse the right sub-tree in in-order

###### Postorder traversal
Traverse the left sub-tree and then traverse the right sub-tree and root respectively. This procedure will be applied to each sub-tree of the tree recursively.

- Traverse the left sub-tree in post-order
- Traverse the right sub-tree in post-order
- visit the root

###### Implementation of CPP
```cpp
#include <iostream>
using namespace std;

struct Node{
	int data;
	struct Node *left, *right;

	Node(int data) {
		this->data = data;
		left = right = NULL;
	}
};

void preorder(struct Node *node) {
	if(node == NULL) {
		return;
	}

	cout << node->data << "\t";
	preorder(node->left);
	preorder(node->right);
}

void inorder(struct Node *node) {
	if(node == NULL) {
		return;
	}

	inorder(node->left);
	cout << node->data << "\t";
	inorder(node->right);
}

void postorder(struct Node *node) {
	if(node == NULL) {
		return;
	}

	postorder(node->left);
	postorder(node->right);
	cout << node->data << "\t";
}

int main() {
	struct Node *root = new Node(1);
	root->left = new Node(2);
	root->right = new Node(3);
	root->left->left = new Node(4);
	root->left->right = new Node(5);

	cout << "Preorder traversal of binary tree is: " << endl;
	preorder(root);
	cout << "\n";

	cout << "Inorder traversal of binary tree is: " << endl;
	inorder(root);
	cout << "\n";

	cout << "Postorder traversal of binary tree is: " << endl;
	postorder(root);
	cout << "\n";

	return 0;
}
```

#### Breadth First Traversal
Level order traversal of a tree is breadth first traversal for the tree.

![ZAnw6I.gif](https://s2.ax1x.com/2019/06/24/ZAnw6I.gif)

Level Order Traversal : 1 2 3 4 5

###### Implementation of Level Order Traversal in CPP
```cpp
#include <iostream>
using namespace std;

class node {
	public:
		int data;
		node *left, *right;
};

node *newNode(int data) {
	node *Node = new node();
	Node->data = data;
	Node->left = NULL;
	Node->right = NULL;

	return(Node);
}

//Compute the "height" of a tree -- the number of
//nodes along the longest path from the root node
//down to the farthest leaf node
int getTreeHeight(node *oneNode) {
	if(oneNode == NULL) {
		return 0;
	} else {
		int leftHeight = getTreeHeight(oneNode->left);
		int rightHeight = getTreeHeight(oneNode->right);

		if(leftHeight > rightHeight) {
			return leftHeight+1;
		} else {
			return rightHeight+1;
		}
	}
}

void printLevelNodes(node *root, int level) {
	if(root == NULL) {
		return;
	} else if(level == 1) {
		cout << root->data << "\t";
	} else if(level > 1){
		printLevelNodes(root->left, level-1);
		printLevelNodes(root->right, level-1);
	}
}

void iterateLevels(node *root) {
	int height = getTreeHeight(root);

	for(int i = 1;i <= height;++i) {
		printLevelNodes(root, i);
	}
}

int main() {
	node *root = newNode(1);
	root->left = newNode(2);
	root->right = newNode(3);
	root->left->left = newNode(4);
	root->left->right = newNode(5);

	cout << "Level Order Traverse of Binary Tree: " << endl;
	iterateLevels(root);

	return 0;
}
```

## Binary Tree representation
There are two types of representation of a binary tree:

#### Linked Representation
In this representation, the binary tree is stored in the memory, in the form of a linked list where the number of nodes are stored at non-contiguous memory locations and linked together by inheriting parent child relationship like a tree.

every node contains three parts : `pointer to the left node`, `data element` and `pointer to the right node`. Each binary tree has a root pointer which points to the root node of the binary tree. In an empty binary tree, the root pointer will point to `null`.

Consider the binary tree given in the figure below.

[![ZkXha8.md.png](https://s2.ax1x.com/2019/06/24/ZkXha8.md.png)](https://imgchr.com/i/ZkXha8)

In the above figure, a tree is seen as the collection of nodes where each node contains three parts : left pointer, data element and right pointer. `Left pointer` stores the address of the left child while `the right pointer` stores the address of the right child. `The leaf node` contains null in its left and right pointers.

The following image shows about how the memory will be allocated for the binary tree by using linked representation. There is a special pointer maintained in the memory which points to the root node of the tree. Every node in the tree contains the address of its left and right child. Leaf node contains null in its left and right pointers.

[![ZkjIw6.md.png](https://s2.ax1x.com/2019/06/24/ZkjIw6.md.png)](https://imgchr.com/i/ZkjIw6)

#### Sequential Representation
This is the simplest memory allocation technique to store the tree elements but it is an inefficient technique since it requires a lot of space to store the tree elements. A binary tree is shown in the following figure along with its memory allocation.

![ZkjOld.png](https://s2.ax1x.com/2019/06/24/ZkjOld.png)

In this representation, an array is used to store the tree elements. Size of the array will be equal to the number of nodes present in the tree. The root node of the tree will be present at the 1st index of the array. If a node is stored at ith index then its left and right children will be stored at 2i and 2i+1 location. If the 1st index of the array i.e. tree[1] is 0, it means that the tree is empty.
