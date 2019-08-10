---
layout: post
title: (DS Linked List)Doubly Linked List
subtitle: Data Structure Linked List
date: 2019-06-20
author: Jalever
header-img: img/post-bg-business-sketchees.jpg
catalog: true
tags:
  - Data Structure
---
- [Overview](#overview)
- [Structure of Node](#structure-of-node)
    - [Node Creation](#node-creation)
    - [Insertion at beginning](#insertion-at-beginning)
        - [Allocate the space](#allocate-the-space)
        - [head is NULL](#head-is-null)
        - [head is not NULL](#head-is-not-null)
        - [Complete Codes](#complete-codes)
    - [Insertion at end](#insertion-at-end)
        - [Allocate the Space inserting into end](#allocate-the-space-inserting-into-end)
        - [head is NULL inserting into end](#head-is-null-inserting-into-end)
        - [head is not NULL inserting into end](#head-is-not-null-inserting-into-end)
        - [Complete Codes inserting into end](#complete-codes-inserting-into-end)
    - [Insertion after specified node](#insertion-after-specified-node)
        - [Complete Codes of inserting at specified node](#complete-codes-of-inserting-at-specified node)
    - [Deletion at beginning](#deletion-at-beginning)
        - [Complete Codes of deleting the first node](#complete-codes-of-deleting-the-first-node)
    - [Deletion at the end](#deletion-at-the-end)
        - [Head is NULL before deletion at the end](#head-is-null-before-deletion-at-the-end)
        - [Head is not NULL before deletion at the end](#head-is-not-null-before-deletion-at-the-end)
        - [Delete Specified Node](#delete-specified-node)
        - [Complete Codes of Deletion at the End](#complete-codes-of-deletion-at-the-end)
    - [Deletion of the node having given data](#deletion-of-the-node-having-given-data)
        - [Complete Codes of Deleting Specified Node](#complete-codes-of-deleting-specified-node)
    - [Searching](#searching)
    - [Traversing](#traversing)
- [Source Codes](#source-codes)

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

###### Complete Codes
```cpp
void InsertAtBeginning() {
	struct node *ptr;
	ptr = (struct node*)malloc(sizeof(struct node));
	int data;

	if(ptr == NULL) {
		cout << "OVERFLOW" << endl;
	} else {
		cout << "Enter a Value: ";
		cin >> data;

		if(head == NULL) {
			ptr->prev = NULL;
			ptr->data = data;
			ptr->next = NULL;

			head = ptr;
		} else {
			ptr->prev = NULL;
			ptr->data = data;

			ptr->next = head;
			head->prev = ptr;

			head = ptr;
		}

		cout << "The data is inserted." << endl;
	}
}
```

#### Insertion at end
In order to insert a node in doubly linked list at the end, we must make sure whether the list is empty or it contains any element. Use the following steps in order to insert the node in doubly linked list at the end.

###### Allocate the Space inserting into end
Allocate the memory for the new node. Make the pointer ptr point to the new node being inserted.
```cpp
ptr = (struct node *) malloc(sizeof(struct node));  
```

###### head is NULL inserting into end
Check whether the list is empty or not. The list is empty if the condition head == NULL holds. In that case, the node will be inserted as the only node of the list and therefore the prev and the next pointer of the node will point to NULL and the head pointer will point to this node.
```cpp
ptr->next = NULL;  
ptr->prev=NULL;  
ptr->data=item;  
head=ptr;  
```

###### head is not NULL inserting into end

In the second scenario, the condition `head == NULL` become false. The new node will be inserted as the last node of the list. For this purpose, we have to traverse the whole list in order to reach the last node of the list. Initialize the pointer temp to head and traverse the list by using this pointer.

```cpp
Temp = head;   
while (temp != NULL) {  
    temp = temp->next;   
}  
```

the pointer temp point to the last node at the end of this while loop. Now, we just need to make a few pointer adjustments to insert the new node ptr to the list. First, make the next pointer of temp point to the new node being inserted i.e. ptr.

```cpp
temp->next =ptr;   
```

make the previous pointer of the node ptr point to the existing last node of the list i.e. temp.

```cpp
ptr->prev = temp;   
```

make the next pointer of the node ptr point to the null as it will be the new last node of the list.

```cpp
ptr->next = NULL   
```

###### Complete Codes inserting into end
```cpp
void InsertingAtLast() {
	struct node *ptr, *last;
	ptr = (struct node*)malloc(sizeof(struct node));
	int data;

	if(ptr == NULL) {
		cout << "OVERFLOW" << endl;
	} else {
		cout << "Enter a Value: " << endl;
		cin >> data;

		if(head == NULL) {
			ptr->prev = NULL;
			ptr->data = data;
			ptr->next = NULL;
			head = ptr;
		} else {
			last = head;

			while(last->next !=NULL) {
				last = last->next;
			}

			ptr->prev = last;
			ptr->data = data;
			ptr->next = NULL;
			last->next = ptr;
		}
		cout << "Node Inserted." << endl;
	}
}
```

#### Insertion after specified node
In order to insert a node after the specified node in the list, we need to skip the required number of nodes in order to reach the mentioned node and then make the pointer adjustments as required.

Use the following steps for this purpose.

Allocate the memory for the new node. Use the following statements for this.
```cpp
ptr = (struct node *)malloc(sizeof(struct node));  
```

Traverse the list by using the pointer temp to skip the required number of nodes in order to reach the specified node.

```cpp
temp=head;  
for(i=0;i<loc;i++) {  
    temp = temp->next;  
    if(temp == NULL) // the temp will be //null if the list doesn't last long //up to mentioned location {  
        return;  
    }  
}  
```

The temp would point to the specified node at the end of the for loop. The new node needs to be inserted after this node therefore we need to make a fer pointer adjustments here. Make the next pointer of ptr point to the next node of temp.

```cpp
ptr->next = temp->next;   
```


make the prev of the new node ptr point to temp.

```cpp
ptr->prev = temp;   
```

make the next pointer of temp point to the new node ptr.

```cpp
temp->next = ptr;   
```

make the previous pointer of the next node of temp point to the new node.

```cpp
temp->next->prev = ptr;    
```

![VzK6mj.png](https://s2.ax1x.com/2019/06/21/VzK6mj.png)

###### Complete Codes of inserting at specified node
```cpp
void InsertAfterSpecificPosition() {
	struct node *ptr, *temp;
	ptr = (struct node*)malloc(sizeof(struct node));
	int data,location;

	if(ptr == NULL) {
		cout << "OVERFLOW" << endl;
	} else {
		cout << "Enter a Value: " << "\t";
		cin >> data;

		cout << "Enter a Position: " << "\t";
		cin >> location;

		temp = head;
		for(int i = 0;i < location;++i) {
			temp = temp->next;
			if(temp == NULL) {
				cout << "Invalid Position for inserting." << endl;
				return;
			}
		}

		ptr->data = data;
		ptr->next = temp->next;
		ptr->prev = temp;

		temp->next = ptr;
		temp->next->prev = ptr;

		cout << "Node Inserted Successfully!" << endl;
	}
}
```

#### Deletion at beginning
Deletion in doubly linked list at the beginning is the simplest operation. We just need to copy the head pointer to pointer `ptr` and shift the head pointer to its next.

```cpp
ptr = head;  
head = head → next;  
```

now make the `prev` of this new head node point to `NULL`. This will be done by using the following statements.

```cpp
head->prev = NULL  
```

Now free the pointer `ptr` by using the free function.

```cpp
free(ptr)
```

###### Complete Codes of deleting the first node
```cpp
void DeleteAtBeginning() {
	struct node* ptr;

	if(head == NULL) {
		cout << "OVERFLOW" << endl;
	} else if(head->next == NULL) {
		head = NULL;
		free(head);
		cout << "The first node has been deleted!" << endl;
	} else {
		ptr = head;
		head = head->next;
		head->prev = NULL;
		free(ptr);

		cout << "The first node has been deleted!" << endl;
	}
}
```

#### Deletion at the end
Deletion of the last node in a doubly linked list needs traversing the list in order to reach the last node of the list and then make pointer adjustments at that position.

In order to delete the last node of the list, we need to follow the following steps.

###### Head is NULL before deletion at the end

If the list is already empty then the condition head == NULL will become true and therefore the operation can not be carried on.

###### Head is not NULL before deletion at the end
If there is only one node in the list then the condition `head->next == NULL` become true. In this case, we just need to assign the head of the list to `NULL` and free head in order to completely delete the list.

###### Delete Specified Node
Otherwise, just traverse the list to reach the last node of the list. This will be done by using the following statements.

```cpp
ptr = head;   
if(ptr->next != NULL) {  
    ptr = ptr -> next;   
}  
```

The `ptr` would point to the last node of the ist at the end of the for loop. Just make the next pointer of the previous node of ptr to `NULL`.

```cpp
ptr → prev → next = NULL  
```

free the pointer as this the node which is to be deleted.

```cpp
free(ptr)     
```

###### Complete Codes of Deletion at the End
```cpp
void DeleteTheLastNode() {
	struct node* ptr;

	if(head == NULL) {
		cout << "OVERFLOW" << endl;
	} else if(head->next == NULL) {
		head = NULL;
		free(head);
		cout << "The last node has been deleted!" << endl;
	} else {
		ptr = head;

		while(ptr->next != NULL) {
			ptr = ptr->next;
		}

		ptr->prev->next = NULL;
		free(ptr);

		cout << "The last node has been deleted!" << endl;
	}
}
```

#### Deletion of the node having given data
In order to delete the node after the specified data, we need to perform the following steps.

Copy the head pointer into a temporary pointer temp.

```cpp
temp = head;
```

Traverse the list until we find the desired data value.

```cpp
while(ptr->data != value) {
	ptr = ptr->next;
}
```

Check if this is the last node of the list. If it is so then we can't perform deletion.

```cpp
if(temp -> next == NULL) {  
    return;   
}
```

Check if the node which is to be deleted, is the last node of the list, if it so then we have to make the next pointer of this node point to null so that it can be the new last node of the list.

```cpp
if(ptr->next->next == NULL) {
	ptr->next = NULL;
}
```

Otherwise, make the pointer ptr point to the node which is to be deleted. Make the next of temp point to the next of ptr. Make the previous of next node of ptr point to temp. free the ptr.
```cpp
temp = ptr->next;
ptr->prev->next = temp;
temp->prev = ptr->prev;
free(ptr);
cout << "Delete Successfully!" << endl;
```

[![VzN1L6.md.png](https://s2.ax1x.com/2019/06/21/VzN1L6.md.png)](https://imgchr.com/i/VzN1L6)

###### Complete Codes of Deleting Specified Node
```cpp
void DeleteTheSpecificNode() {
	struct node *ptr, *temp;

	int value;
	cout << "Enter the value that you want to delete" << "\t";
	cin >> value;

	ptr = head;
	while(ptr->data != value) {
		ptr = ptr->next;
	}

	if(ptr->next == NULL) {
		cout << "It cann't be deleted." << endl;
	} else if(ptr->next->next == NULL) {
		ptr->next = NULL;
	} else {
		temp = ptr->next;
		ptr->prev->next = temp;
		temp->prev = ptr->prev;
		free(ptr);
		cout << "Delete Successfully!" << endl;
	}
}
```

#### Searching
```cpp
void Search() {
	struct node *ptr;
	int value, isFound = 0,location = 0;

	ptr = head;

	if(ptr == NULL) {
		cout << "Empty List!" << endl;
	} else {
		cout << "Enter the value you want to look for: " << endl;
		cin >> value;

		while(ptr != NULL) {
			if(ptr->data == value) {
				cout << "value has been found.location is " << location+1 << endl;
				isFound = 1;
				break;
			} else {
				isFound = 0;
			}

			location += 1;
			ptr = ptr->next;
		}


		if(isFound == 0) {
			cout << "Value can not be found." << endl;
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
	while(ptr != NULL) {
		cout << ptr->data << " -> ";
		ptr = ptr->next;
	}
}
```

## Source Codes
[Complete Operations Implementating in CPP](https://github.com/Jalever/Data-Structure-and-Algorithm/blob/master/Data%20Structure/Linked%20List/Doubly%20Linked%20List.cpp)
