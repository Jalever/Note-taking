---
layout: post
title: (DS Linked List)Circular Doubly Linked List
subtitle: Data Structure Linked List学习笔记系列
date: 2019-06-23
author: Jalever
header-img: img/home-bg2.jpg
catalog: true
tags:
  - Data Structure
---

- [Introduction](#introduction)
- [Operations](#operations)
- [Insertion at beginning](#insertion-at-beginning)
    - [Scenario 1 of insertion at beginning](#scenario-1-of-insertion-at-beginning)
    - [Scenario 2 of insertion at beginning](#scenario-2-of-insertion-at-beginning)
    - [Source codes of insertion at beginning](#source-codes-of-insertion-at-beginning)






## Introduction

Circular doubly linked list is a more complexed type of data structure in which a node contain pointers to its previous node as well as the next node. Circular doubly linked list doesn't contain NULL in any of the node. The last node of the list contains the address of the first node of the list. The first node of the list also contain address of the last node in its previous pointer.

A circular doubly linked list is shown in the following figure.

[![ZCa1G8.md.png](https://s2.ax1x.com/2019/06/23/ZCa1G8.md.png)](https://imgchr.com/i/ZCa1G8)

Due to the fact that a circular doubly linked list contains three parts in its structure therefore, it demands more space per node and more expensive basic operations. However, a circular doubly linked list provides easy manipulation of the pointers and the searching becomes twice as efficient.

## Operations

#### Insertion at beginning
There are two scenario of inserting a node in circular doubly linked list at beginning. Either the list is empty or it contains more than one element in the list.

Allocate the memory space for the new node `ptr` by using the following statement.

```cpp
ptr = (struct node *)malloc(sizeof(struct node));  
```

![ZCD7VJ.png](https://s2.ax1x.com/2019/06/23/ZCD7VJ.png)

###### Scenario 1 of insertion at beginning
In the first case, the condition `head == NULL` becomes true therefore, the node will be added as the first node in the list. The next and the previous pointer of this newly added node will point to itself only. This can be done by using the following statement.

```cpp
head = ptr;  
ptr -> next = head;   
ptr -> prev = head;
```

###### Scenario 2 of insertion at beginning
In the second scenario, the condition `head == NULL` becomes false. In this case, we need to make a few pointer adjustments at the end of the list. For this purpose, we need to reach the last node of the list through traversing the list. Traversing the list can be done by using the following statements.
```cpp
temp = head;   
while(temp -> next != head) {  
    temp = temp -> next;   
}  
```

At the end of loop, the pointer temp would point to the last node of the list. Since the node which is to be inserted will be the first node of the list therefore, temp must contain the address of the new node ptr into its next part. All the pointer adjustments can be done by using the following statements.

[![ZCruZQ.md.png](https://s2.ax1x.com/2019/06/23/ZCruZQ.md.png)](https://imgchr.com/i/ZCruZQ)

```cpp
lastNode -> next = ptr;  
ptr -> prev = lastNode;  
head -> prev = ptr;  
ptr -> next = head;  
head = ptr;  
```

In this way, the new node is inserted into the list at the beginning. The algorithm and its C implementation is given as follows.

###### Source codes of insertion at beginning
```cpp
void InsertAtBeginning() {
	struct node *ptr, *lastNode;
	ptr = (struct node*)malloc(sizeof(struct node));

	int data;

	if(ptr == NULL) {
		cout << "OVERFLOW" << endl;
	} else {
		cout << "Enter a Value: ";
		cin >> data;

		ptr->data = data;

		if(head == NULL) {
			head = ptr;
			ptr->prev = head;
			ptr->next = head;
		} else {

			lastNode = head;
			while(lastNode->next != head) {
				lastNode = lastNode->next;
			}

			lastNode->next = ptr;
			ptr->prev = lastNode;
			head->prev = ptr;
			ptr->next = head;

			ptr = head;
		}

		cout << "OVERFLOW" << endl;
	}
}
```

#### Insertion at end



#### Deletion at beginning



#### Deletion at end
