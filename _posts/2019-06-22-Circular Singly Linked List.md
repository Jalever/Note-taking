---
layout: post
title: Circular Singly Linked List
subtitle: Data Structure Linked List学习笔记系列
date: 2019-06-22
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Data Structure
---
- [Introduction](#introduction)
- [Usage](#usage)
- [Operations](#operations)
    - [Insertion at beginning](#insertion-at-beginning)
        - [Allocate the space when inserting at beginning](#allocate-the-space-when-inserting-at-beginning)
        - [head is NULL when inserting at beginning](#head-is-null-when-inserting-at-beginning)
        - [head is not NULL when inserting at beginning ](#head-is-not-null-when-inserting-at-bginning )
        - [Source codes of insertion at beginning](#source-codes-of-insertion-at-beginning)
    - [Insertion at the end](#insertion-at-the-end)
        - [Allocate the Space](#allocate-the-space)
        - [head is NULL while inserting at the end](#head-is-null-while-inserting-at-the-end)
        - [head is not NULL while inserting at the end](#head-is-not-null-while-inserting-at-the-end)
        - [Source codes of insertion at the end](#source-codes-of-insertion-at-the-end)
    - [Deletion at beginning](#deletion-at-beginning)
        - [Empty list while deleting the first node](#empty-list-while-deleting-the-first-node)    
        - [Single node while deleting the first node](#single-node-while-deleting-the-first-node)
        - [More than one node while deleting the first node](#more-than-one-node-while-deleting-the-first-node)
        - [Source codes of deletion the first node](#source-codes-of-deletion-the-first-node)
    - [Deletion at the end](#deletion-at-the-end)
        - [Empty list while deleting the last node](#empty-list-while-deleting-the-last-node)
        - [Single node while deleting the last node](#single-node-while-deleting-the-last-node)
        - [More than one node while deleting the last node](#more-than-one-node-while-deleting-the-last-node)
        - [Source codes of deletion the last node](#source-codes-of-deletion-the-last-node)
    - [Searching](#searching)
    - [Traversing](#traversing)
- [Links](#links)

## Introduction
In a circular Singly linked list, the last node of the list contains a pointer to the first node of the list.

We traverse a circular singly linked list until we reach the same node where we started. The circular singly liked list has no beginning and no ending. There is no null value present in the next part of any of the nodes.

The following image shows a circular singly linked list.

[![Zpx991.md.png](https://s2.ax1x.com/2019/06/22/Zpx991.md.png)](https://imgchr.com/i/Zpx991)

## Usage
Circular linked list are mostly used in task maintenance in operating systems. There are many examples where circular linked list are being used in computer science including browser surfing where a record of pages visited in the past by the user, is maintained in the form of circular linked lists and can be accessed again on clicking the previous button.

## Operations

#### Insertion at beginning
There are two scenario in which a node can be inserted in circular singly linked list at beginning. Either the node will be inserted in an empty list or the node is to be inserted in an already filled list.

###### Allocate the space when inserting at beginning
Firstly, allocate the memory space for the new node by using the malloc method of C language.

```cpp
struct node *ptr = (struct node *)malloc(sizeof(struct node));  
```

###### head is NULL when inserting at beginning
In the first scenario, the condition head == NULL will be true. Since, the list in which, we are inserting the node is a circular singly linked list, therefore the only node of the list (which is just inserted into the list) will point to itself only. We also need to make the head pointer point to this node. This will be done by using the following statements.
```cpp
if(head == NULL) {  
    head = ptr;  
    ptr -> next = head;  
}
```

###### head is not NULL when inserting at beginning
In the second scenario, the condition head == NULL will become false which means that the list contains at least one node. In this case, we need to traverse the list in order to reach the last node of the list. This will be done by using the following statement.
```cpp
temp = head;  
while(temp->next != head) {
    temp = temp->next;
}
```

At the end of the loop, the pointer temp would point to the last node of the list. Since, in a circular singly linked list, the last node of the list contains a pointer to the first node of the list. Therefore, we need to make the next pointer of the last node point to the head node of the list and the new node which is being inserted into the list will be the new head node of the list therefore the next pointer of temp will point to the new node ptr.

This will be done by using the following statements.

```cpp
temp -> next = ptr;   
```

the next pointer of temp will point to the existing head node of the list.

```cpp
ptr->next = head;   
```

Now, make the new node ptr, the new head node of the circular singly linked list.

```cpp
head = ptr;  
```

in this way, the node ptr has been inserted into the circular singly linked list at beginning.


![ZpMqqe.png](https://s2.ax1x.com/2019/06/22/ZpMqqe.png)

###### Source codes of insertion at beginning
```cpp
void InsertAtBeginning() {
	struct node *ptr, *temp;
	ptr = (struct node*)malloc(sizeof(struct node));

	int data;

	if(ptr == NULL) {
		cout << "OVERFLOW!" << endl;
	} else {
		cout << "Enter a Value: ";
		cin >> data;

		ptr->data = data;

		if(head == NULL) {
			head = ptr;
			ptr->next = head;
		} else {
			temp = head;
			while(temp->next != head) {
				temp = temp->next;
			}

			ptr->next = head;
			temp->next = ptr;
			head = ptr;
		}

		cout << "\nNode Inserted." << endl;
	}
}
```

#### Insertion at the end
There are two scenario in which a node can be inserted in circular singly linked list at beginning. Either the node will be inserted in an empty list or the node is to be inserted in an already filled list.

###### Allocate the Space
Firstly, allocate the memory space for the new node by using the malloc method of C language.

```cpp
struct node *ptr = (struct node *)malloc(sizeof(struct node));  
```

###### head is NULL while inserting at the end

In the first scenario, the condition head == NULL will be true. Since, the list in which, we are inserting the node is a circular singly linked list, therefore the only node of the list (which is just inserted into the list) will point to itself only. We also need to make the head pointer point to this node. This will be done by using the following statements.
```cpp
if(head == NULL) {  
    head = ptr;  
    ptr -> next = head;  
}
```

###### head is not NULL while inserting at the end
In the second scenario, the condition head == NULL will become false which means that the list contains at least one node. In this case, we need to traverse the list in order to reach the last node of the list. This will be done by using the following statement.

```cpp
temp = head;  
while(temp->next != head) {
   temp = temp->next;  
}
```

At the end of the loop, the pointer temp would point to the last node of the list. Since, the new node which is being inserted into the list will be the new last node of the list. Therefore the existing last node i.e. temp must point to the new node `ptr`. This is done by using the following statement.

```cpp
temp -> next = ptr;   
```

The new last node of the list i.e. `ptr` will point to the head node of the list.

```cpp
ptr -> next = head;  
```

In this way, a new node will be inserted in a circular singly linked list at the beginning.

###### Source codes of insertion at the end
```cpp
void InsertAtLast() {
	struct node *ptr, *temp;

	ptr = (struct node*)malloc(sizeof(struct node));

	int data;

	if(ptr == NULL) {
		cout << "OVERFLOW, you have to execute InsertAtBeginning firstly." << endl;
	} else {
		cout << "Enter a value: ";
		cin >> data;

		if(head == NULL) {
			ptr->next = head; //circular linked list
			ptr->data = data;
			head = ptr;
		} else {
			temp = head;
			while(temp->next != head) {
				temp = temp->next;
			}

			temp->next = ptr;
			ptr->data = data;
			ptr->next = head;
		}
	}

	cout << "Node Inserted!" << endl;
}
```

#### Deletion at the end
There are three scenarios of deleting a node in circular singly linked list at the end.

###### Empty list while deleting the last node
If the list is empty then the condition `head == NULL` will become true, in this case, we just need to print underflow on the screen and make exit.

```cpp
if(head == NULL) {  
    printf("\nUNDERFLOW");    
    return;   
}  
```

###### Single node while deleting the last node
If the list contains single node then, the condition `head->next == head` will become true. In this case, we need to delete the entire list and make the head pointer free. This will be done by using the following statements.

```cpp
if(head->next == head) {  
    head = NULL;  
    free(head);  
}
```

###### More than one node while deleting the last node
If the list contains more than one element, then in order to delete the last element, we need to reach the last node. We also need to keep track of the second last node of the list. For this purpose, the two pointers `lastOne` and `lastTwo` are defined. The following sequence of code is used for this purpose.

```cpp
lastOne = head;
while(lastOne->next != head) {
	lastTwo = lastOne;
	lastOne = lastOne->next;
}
```

now, we need to make just one more pointer adjustment. We need to make the next pointer of `lastTwo` point to the next of `lastOne` (i.e. head) and then make pointer `lastOne` free.

```cpp
lastTwo->next = lastOne->next;
free(lastOne);
```

###### Source codes of deletion the last node
```cpp
void DeleteTheLastNode() {
	struct node *lastTwo, *lastOne;

	if(head == NULL) {
		cout << "UNDERFLOW" << endl;
	} else if(head->next == head) {
		head = NULL;
		free(head);
		cout << "The only node has been deleted." << endl;
	} else {
		lastOne = head;
		while(lastOne->next != head) {
			lastTwo = lastOne;
			lastOne = lastOne->next;
		}

		lastTwo->next = lastOne->next;
		free(lastOne);

		cout << "The last one node has been deleted." << endl;
	}
}
```

#### Deletion at the end
In order to delete a node in circular singly linked list, we need to make a few pointer adjustments.

There are three scenarios of deleting a node from circular singly linked list at beginning.

###### Empty list while deleting the first node
If the list is empty then the condition head == NULL will become true, in this case, we just need to print underflow on the screen and make exit.

```cpp
if(head == NULL) {  
    printf("\nUNDERFLOW");    
    return;   
}
```

###### Single node while deleting the first node
If the list contains single node then, the condition head → next == head will become true. In this case, we need to delete the entire list and make the head pointer free. This will be done by using the following statements.

```cpp
if(head->next == head) {  
    head = NULL;  
    free(head);  
}  
```

###### More than one node while deleting the first node
If the list contains more than one node then, in that case, we need to traverse the list by using the pointer `ptr` to reach the last node of the list. This will be done by using the following statements.

```cpp
ptr = head;   
while(ptr -> next != head) {
       ptr = ptr -> next;   
}
```

At the end of the loop, the pointer `ptr` point to the last node of the list. Since, the last node of the list points to the head node of the list. Therefore this will be changed as now, the last node of the list will point to the next of the head node.

```cpp
ptr->next = head->next;  
```

Now, free the head pointer by using the `free()` method in C language.

```cpp
free(head);  
```

Make the node pointed by the next of the last node, the new head of the list.

```cpp
head = ptr->next;  
```

In this way, the node will be deleted from the circular singly linked list from the beginning.

###### Source codes of deletion the first node
```cpp
void DeleteTheFirstNode() {
	struct node *ptr;

	if(head == NULL) {
		cout << "UNDERFLOW" << endl;
	} else if(head->next == head){
		head = NULL;
		free(head);
		cout << "The first node has been deleted.";
	} else {
		ptr = head;
		while(ptr->next != head) {
			ptr = ptr->next;
		}

		ptr->next = head->next;
		free(head);
		head = ptr->next;

		cout << "The first node has been deleted." << endl;
	}
}
```

#### Searching
```cpp
void Search() {
	int data, isFound = 0,location = 0;

	struct node *ptr;

	ptr = head;
	if(ptr == NULL) {
		cout << "OVERFLOW" << endl;
	} else {
		cout << "Enter the value you wanna look for: " << endl;
		cin >> data;

		if(head->data == data) {
			cout << "The value has been found." << location+1 << endl;
			isFound = 1;
		} else {
			while(ptr->next != head) {
				if(ptr->data == data) {
					cout << "The value has been found." << location+1 << endl;
					isFound = 1;
					break;
				} else {
					isFound = 0;
				}

				location++;
				ptr = ptr->next;
			}

			if(isFound != 0) {
				cout << "the value haven't been found." << endl;
			}
		}

	}
}
```

#### Traversing
```cpp
void Traverse() {
	struct node *ptr;
	ptr = head;

	cout << "The Doubly Linked List is: " << endl;
	if(head == NULL) {
		cout << "Empty List." << endl;
	} else {
		cout << "Printing Values..." << endl;
		while(ptr->next != head) {
			cout << ptr->data << " -> ";
			ptr = ptr->next;
		}
		cout << " " << ptr->data;
	}
}
```

## Links
[All Source Codes of Circular Singly Linked List](https://github.com/Jalever/Data-Structure-and-Algorithm/blob/master/Data%20Structure/Linked%20List/Circular%20Singly%20Linked%20List.cpp)
