---
layout: post
title: (DS Tree)Binary Search Tree
subtitle: Data Structure Tree学习笔记系列
date: 2019-06-27
author: Jalever
header-img: img/post-bg-star.jpg
catalog: true
tags:
  - Data Structure
---

## Overview

1. Binary Search tree can be defined as a class of binary trees, in which the nodes are arranged in a specific order. This is also called ordered binary tree.

2. In a binary search tree, the value of all the nodes in the left sub-tree is less than the value of the root.

3. Similarly, value of all the nodes in the right sub-tree is greater than or equal to the value of the root.

4. This rule will be recursively applied to all the left and right sub-trees of the root.

![ZnCFBT.png](https://s2.ax1x.com/2019/06/27/ZnCFBT.png)

A Binary search tree is shown in the above figure. As the constraint applied on the BST, we can see that the root node 30 doesn't contain any value greater than or equal to 30 in its left sub-tree and it also doesn't contain any value less than 30 in its right sub-tree.

## Advantages of using binary search tree
1. Searching become very efficient in a binary search tree since, we get a hint at each step, about which sub-tree contains the desired element.
2. The binary search tree is considered as efficient data structure in compare to arrays and linked lists. In searching process, it removes half sub-tree at every step. Searching for an element in a binary search tree takes o(log2n) time. In worst case, the time it takes to search an element is 0(n).
3. It also speed up the insertion and deletion operations as compare to that in array and linked list.

## Example of creating Binary Search Tree using the following data elements
```text
43, 10, 79, 90, 12, 54, 11, 9, 50
```

1. Insert 43 into the tree as the root of the tree.
2. Read the next element, if it is lesser than the root node element, insert it as the root of the left sub-tree.
3. Otherwise, insert it as the root of the right of the right sub-tree.

The process of creating BST by using the given elements, is shown in the image below.

[![ZnZC01.md.png](https://s2.ax1x.com/2019/06/27/ZnZC01.md.png)](https://imgchr.com/i/ZnZC01)

## Operations on Binary Search Tree

#### Searching in BST


#### Insertion in BST


#### Deletion in BST

## Source Codes
```cpp
#include <iostream>
using namespace std;

struct Node{
	Node *left;
	int data;
	Node *right;
};

//---------------Insertion----------------------------
Node *Create(int data){
	Node *node = new Node;
	node->data = data;
	node->left = node->right = NULL;
	return node;
};

Node *Insertion(Node *root,int data) {
	if(root == NULL) {
		return Create(data);
	}

	if(data < root->data) {
		root->left = Insertion(root->left, data);
	} else {
		root->right = Insertion(root->right, data);
	}

	return root;
}

//-------------Deletion------------------------------
void Search(Node *&currentNode,int data,Node *&parentNode) {
	while(currentNode != NULL && currentNode->data != data) {
		parentNode = currentNode;

		if(data < currentNode->data) {
			currentNode = currentNode->left;
		} else {
			currentNode = currentNode->right;
		}
	}
}

Node *getInorderSuccessor(Node *currentNode) {
	while(currentNode->left != NULL) {
		currentNode = currentNode->left;
	}

	return currentNode;
}

void Deletion(Node *&root,int data) {
	Node *parentNode = NULL;
	Node *currentNode = root;

	Search(currentNode,data,parentNode);

	if(currentNode == NULL) {
		return;
	}

//	The node to be deleted is a leaf node
	if(currentNode->left == NULL && currentNode->right == NULL) {
		if(currentNode != root) {
			if(parentNode->left == currentNode) {
				parentNode->left = NULL;
			} else {
				parentNode->right = NULL;
			}
		} else {
			root = NULL;
		}

		free(currentNode);
	} else if(currentNode->left && currentNode->right) {//The node to be deleted has two children
		Node *successor = getInorderSuccessor(currentNode->right);

		int value = successor->data;
		Deletion(root, successor->data);

		currentNode->data = value;
	} else {//The node to be deleted has only one child
		Node *childNode = (currentNode->left)?currentNode->left : currentNode->right;

		if(currentNode != root) {
			if(currentNode == parentNode->left) {
				parentNode->left = childNode;
			} else {
				parentNode->right = childNode;
			}
		} else {
			root = childNode;
		}

		free(currentNode);
	}
}


//-------------Traversal------------------------------

//traversal
void Preorder(Node *root) {
	if(root == NULL) {
		return;
	}

	cout << root->data << " ";
	Preorder(root->left);
	Preorder(root->right);
}

void Inorder(Node *root) {
	if(root == NULL) {
		return;
	}

	Inorder(root->left);
	cout << root->data << " ";
	Inorder(root->right);
}

void Postorder(Node *root) {
	if(root == NULL) {
		return;
	}

	Postorder(root->left);
	Postorder(root->right);
	cout << root->data << " ";
}

//-------------------------------------------

int main() {
	Node *root = NULL;

	int tree[8];

	for(int i = 0;i < 8;++i) {
		cout << "Enter [" << i <<"] Value Inserted: ";
		cin >> tree[i];
		root = Insertion(root, tree[i]);
	}

	cout << "print all values: " << endl;
	cout << "\npreorder: " << endl;
	Preorder(root);
	cout << "\ninorder: " << endl;
	Inorder(root);
	cout << "\npostorder: " << endl;
	Postorder(root);

	cout << "\nprint all nodes after deleting node which value is equivalent to 10: " << endl;
	Deletion(root, 10);
	Inorder(root);

	return 0;
}

```
