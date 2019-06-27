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
- [Overview](#overview)
- [Advantages of using binary search tree](#advantages-of-using-binary-search-tree)
- [Example of creating Binary Search Tree using the following data elements](#example-of-creating-binary-search-tree-using-the-following-data-elements)
- [Operations on Binary Search Tree](#operations-on-binary-search-tree)
    - [Insertion in BST](#insertion-in-bst)
    - [Deletion in BST](#deletion-in-bst)
        - [Prerequisites](#prerequisites)
        - [The node to be deleted is a leaf node](#the-node-to-be-deleted-is-a-leaf-node)
        - [The node to be deleted has only one child](#the-node-to-be-deleted-has-only-one-child)
        - [The node to be deleted has two children](#the-node-to-be-deleted-has-two-children)
- [Source Codes](#source-codes)

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

#### Insertion in BST
Insert function is used to add a new element in a binary search tree at appropriate location. Insert function is to be designed in such a way that, it must node violate the property of binary search tree at each value.

1. Allocate the memory for tree.
2. Set the data part to the value and set the left and right pointer of tree, point to NULL.
3. If the item to be inserted, will be the first element of the tree, then the left and right of this node will point to NULL.
4. Else, check if the item is less than the root element of the tree, if this is true, then recursively perform this operation with the left of the root.
5. If this is false, then perform this operation recursively with the right sub-tree of the root.

```cpp
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
```

#### Deletion in BST
###### Prerequisites
```cpp
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
```

###### The node to be deleted is a leaf node
It is the simplest case, in this case, replace the leaf node with the NULL and simple free the allocated space.

In the following image, we are deleting the node 85, since the node is a leaf node, therefore the node will be replaced with NULL and allocated space will be freed.

[![Zn5TJg.md.png](https://s2.ax1x.com/2019/06/27/Zn5TJg.md.png)](https://imgchr.com/i/Zn5TJg)

```cpp
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
}
```

###### The node to be deleted has only one child
In this case, replace the node with its child and delete the child node, which now contains the value which is to be deleted. Simply replace it with the NULL and free the allocated space.

In the following image, the node 12 is to be deleted. It has only one child. The node will be replaced with its child node and the replaced node 12 (which is now leaf node) will simply be deleted.

[![ZnIQld.md.png](https://s2.ax1x.com/2019/06/27/ZnIQld.md.png)](https://imgchr.com/i/ZnIQld)

```cpp
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
```

###### The node to be deleted has two children
It is a bit complexed case compare to other two cases. However, the node which is to be deleted, is replaced with its in-order successor or predecessor recursively until the node value (to be deleted) is placed on the leaf of the tree. After the procedure, replace the node with NULL and free the allocated space.

In the following image, the node 50 is to be deleted which is the root node of the tree. The in-order traversal of the tree given below.

6, 25, 30, 50, 52, 60, 70, 75.

replace 50 with its in-order successor 52. Now, 50 will be moved to the leaf of the tree, which will simply be deleted.

[![ZnINtS.md.png](https://s2.ax1x.com/2019/06/27/ZnINtS.md.png)](https://imgchr.com/i/ZnINtS)

```cpp
if(currentNode->left && currentNode->right) {
	Node *successor = getInorderSuccessor(currentNode->right);

	int value = successor->data;
	Deletion(root, successor->data);

	currentNode->data = value;
}
```

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

//The node to be deleted is a leaf node

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
	} else {

        //The node to be deleted has only one child

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
