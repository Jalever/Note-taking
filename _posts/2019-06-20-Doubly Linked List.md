---
layout: post
title: (DS Linked List)Doubly Linked List
subtitle: Data Structure Linked List学习笔记系列
date: 2019-06-20
author: Jalever
header-img: img/post-bg-business-sketchees.jpg
catalog: true
tags:
  - Data Structure
---


## Overview
Doubly linked list is a complex type of linked list in which a node contains a pointer to the previous as well as the next node in the sequence.

Therefore, in a doubly linked list, a node consists of three parts:
- node data
- pointer to the next node in sequence (next pointer)
- pointer to the previous node (previous pointer)

A sample node in a doubly linked list is shown in the figure.

![VzC4qU.png](https://s2.ax1x.com/2019/06/21/VzC4qU.png)

A doubly linked list containing three nodes having numbers from 1 to 3 in their data part, is shown in the following image.

[![VzCIZF.md.png](https://s2.ax1x.com/2019/06/21/VzCIZF.md.png)](https://imgchr.com/i/VzCIZF)

## Structure of Node
In C, structure of a node in doubly linked list can be given as :
```cpp
struct node   
{  
    struct node *prev;   
    int data;  
    struct node *next;   
}   
```
The `prev` part of the first node and the `next` part of the last node will always contain null indicating end in each direction.

## Operations

#### Node Creation
```cpp
struct node   
{  
    struct node *prev;  
    int data;  
    struct node *next;  
};  
struct node *head;
```

#### Insertion at beginning
As in doubly linked list, each node of the list contain double pointers therefore we have to maintain more number of pointers in doubly linked list as compare to singly linked list.

There are two scenarios of inserting any element into doubly linked list. Either the list is empty or it contains at least one element.

Perform the following steps to insert a node in doubly linked list at beginning.

###### Allocate the space

Allocate the space for the new node in the memory. This will be done by using the following statement.

```cpp
ptr = (struct node *)malloc(sizeof(struct node));  
```

###### head is NULL

Check whether the list is empty or not. The list is empty if the condition `head == NULL` holds. In that case, the node will be inserted as the only node of the list and therefore the `prev` and the `next` pointer of the node will point to `NULL` and the head pointer will point to this node.

```cpp
ptr->next = NULL;  
ptr->prev=NULL;  
ptr->data=item;  
head=ptr;  
```

###### head is not NULL

In the second scenario, the condition `head == NULL` become false and the node will be inserted in beginning. The next pointer of the node will point to the existing head pointer of the node. The `prev` pointer of the existing head will point to the new node being inserted.

```cpp
ptr->next = head;  
head->prev=ptr;  
```

Since, the node being inserted is the first node of the list and therefore it must contain `NULL` in its `prev` pointer. Hence assign null to its previous part and make the head point to this node.

```cpp
ptr->prev =NULL  
head = ptr
```

[![VzkEsx.md.png](https://s2.ax1x.com/2019/06/21/VzkEsx.md.png)](https://imgchr.com/i/VzkEsx)

#### Insertion at end



#### Insertion after specified node



#### Deletion at beginning


#### delete the last value


#### delete a specified value


#### search specified value in doubly linked list

#### traverse all values
