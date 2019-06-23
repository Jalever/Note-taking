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
    - [Insertion at end](#insertion-at-end)
        - [Scenario 1 of insertion at end](#scenario-1-of-insertion-at-end)
        - [Scenario 2 of insertion at end](#scenario-2-of-insertion-at-end)
        - [Source codes of insertion at end](#source-codes-of-insertion-at-end)
    - [Deletion at beginning](#deletion-at-beginning)
        - [Scenario 1 of deleting at beginning](#scenario-1-of-deleting-at-beginning)
        - [Scenario 2 of deleting at beginning](#scenario-2-of-deleting-at-beginning)
        - [Source codes of deleting at beginning](#source-codes-of-deleting-at-beginning)
    - [Deletion at end](#deletion-at-end)
        - [Scenario 1 of insertion at end](#scenario-1-of-deleting-at-end)
        - [Scenario 2 of insertion at end](#scenario-2-of-deleting-at-end)
        - [Source codes of insertion at end](#source-codes-of-deleting-at-end)
    - [Search](#search)
        - [Source codes of Search](#source-codes-of-search)
- [Links](#links)

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

            head = ptr;
		}

		cout << "OVERFLOW" << endl;
	}
}
```

#### Insertion at end
There are two scenario of inserting a node in circular doubly linked list at the end. Either the list is empty or it contains more than one element in the list.

Allocate the memory space for the new node `ptr` by using the following statement.

```cpp
ptr = (struct node *)malloc(sizeof(struct node));  
```

![ZCD7VJ.png](https://s2.ax1x.com/2019/06/23/ZCD7VJ.png)

###### Scenario 1 of insertion  at end
In the first case, the condition `head == NULL` becomes true therefore, the node will be added as the first node in the list. The next and the previous pointer of this newly added node will point to itself only. This can be done by using the following statement.

```cpp
head = ptr;  
ptr -> next = head;   
ptr -> prev = head;
```

###### Scenario 2 of insertion  at end
In the second scenario, the condition `head == NULL` become false, therefore node will be added as the last node in the list. For this purpose, we need to make a few pointer adjustments in the list at the end. Since, the new node will contain the address of the first node of the list therefore we need to make the next pointer of the last node point to the head node of the list. Similarly, the previous pointer of the head node will also point to the new last node of the list.

```cpp
head -> prev = ptr;  
ptr -> next = head;
```

Now, we also need to make the next pointer of the existing last node of the list (temp) point to the new last node of the list, similarly, the new last node will also contain the previous pointer to the temp. this will be done by using the following statements.

```cpp
temp->next = ptr;  
ptr ->prev=temp;
```

In this way, the new node ptr has been inserted as the last node of the list. The algorithm and its C implementation has been described as follows.

[![ZCruZQ.md.png](https://s2.ax1x.com/2019/06/23/ZCruZQ.md.png)](https://imgchr.com/i/ZCruZQ)

###### Source codes of insertion at beginning
```cpp
void InsertAtLast() {
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
			ptr = head;
			ptr->next = head;
			ptr->prev = head;
		} else {
			lastNode = head;
			while(lastNode->next != head) {
				lastNode = lastNode->next;
			}

			lastNode->next = ptr;
			ptr->prev = lastNode;
			head->prev = ptr;
			ptr->next = head;
		}

		cout << "Node Inserted." << endl;
	}
}
```

#### Deletion at beginning
There can be two scenario of deleting the first node in a circular doubly linked list.

![ZPYfQH.png](https://s2.ax1x.com/2019/06/23/ZPYfQH.png)

###### Scenario 1 of deleting at beginning
The node which is to be deleted can be the only node present in the linked list. In this case, the condition head → next == head will become true, therefore the list needs to be completely deleted.

It can be simply done by assigning head pointer of the list to null and free the head pointer.

```cpp
head = NULL;   
free(head);
```

###### Scenario 2 of deleting at beginning
in the second scenario, the list contains more than one element in the list, therefore the condition `head -> next == head` will become false. Now, reach the last node of the list and make a few pointer adjustments there. Run a while loop for this purpose

```cpp
temp = head;   
while(temp -> next != head) {  
    temp = temp -> next;  
}  
```

Now, temp will point to the last node of the list. The first node of the list i.e. pointed by head pointer, will need to be deleted. Therefore the last node must contain the address of the node that is pointed by the next pointer of the existing head node. Use the following statement for this purpose.

```cpp
temp -> next = head -> next;  
```

The new head node i.e. next of existing head node must also point to the last node of the list through its previous pointer. Use the following statement for this purpose.

```cpp
head -> next -> prev = temp;  
```

Now, free the head pointer and the make its next pointer, the new head node of the list.

```cpp
free(head);  
head = temp -> next;  
```

in this way, a node is deleted at the beginning from a circular doubly linked list.

[![ZPUnJK.md.png](https://s2.ax1x.com/2019/06/23/ZPUnJK.md.png)](https://imgchr.com/i/ZPUnJK)
###### Source codes of deleting at beginning
```cpp
void DeleteAtBeginning() {
	struct node *lastNode;

	if(head == NULL) {
		cout << "Empty List" << endl;
	} else if(head->next == NULL) {
		head = NULL;
		free(head);
		cout << "The only node has been deleted.";
	} else {
		lastNode = head;
		while(lastNode->next != head) {
			lastNode = lastNode->next;
		}

		lastNode->next = head->next;
		head->next->prev = lastNode;
		free(head);
		head = lastNode->next;
	}
}
```

#### Deletion at end
There can be two scenario of deleting the first node in a circular doubly linked list.

![ZPYfQH.png](https://s2.ax1x.com/2019/06/23/ZPYfQH.png)

###### Scenario 1 of deleting at end
The node which is to be deleted can be the only node present in the linked list. In this case, the condition `head -> next == head` will become true, therefore the list needs to be completely deleted.

It can be simply done by assigning head pointer of the list to null and free the head pointer.

```cpp
head = NULL;   
free(head);
```

###### Scenario 2 of deleting at end
in the second scenario, the list contains more than one element in the list, therefore the condition `head -> next == head` will become false. Now, reach the last node of the list and make a few pointer adjustments there. Run a while loop for this purpose

```cpp
temp = head;   
while(temp -> next != head) {  
    temp = temp -> next;  
}  
```

Now, temp will point to the node which is to be deleted from the list. Make the next pointer of previous node of temp, point to the head node of the list.

```cpp
temp -> prev -> next = head;  
```

make the previous pointer of the head node, point to the previous node of temp.

```cpp
head -> prev = ptr -> prev;    
```

Now, free the temp pointer to free the memory taken by the node.

```cpp
free(head)  
```

in this way, the last node of the list is deleted.

[![ZPBjZ4.md.png](https://s2.ax1x.com/2019/06/23/ZPBjZ4.md.png)](https://imgchr.com/i/ZPBjZ4)

###### Source codes of deleting at end
```cpp
void DeleteAtLast() {
	struct node *lastNode;

	if(head == NULL) {
		cout << "Empty List" << endl;
	} else if(head->next == NULL) {
		head = NULL;
		free(head);
		cout << "The only node has been deleted.";
	} else {
		lastNode = head;
		while(lastNode->next != head) {
			lastNode = lastNode->next;
		}

		lastNode->prev->next = head;
		head->prev = lastNode->prev;

		free(lastNode);

		cout << "The node has been deleted." << endl;
	}
}
```

#### Search

###### Source codes of Search
```cpp
void Search() {
	int data, location = 0, isFound = 0;
	struct node *ptr;

	ptr = head;
	if(ptr == NULL) {
		cout << "Empty List" << endl;
	} else {
		cout << "Enter a value that you want to find it: ";
		cin >> data;

		if(head->data == data) {
			isFound = 1;
			cout << "Found it, location is: " << location+1 << endl;
		} else {

			while(ptr->next != head) {
				if(ptr->data == data) {
					cout << "Found it, location is: " << location+1 << endl;
					isFound = 1;
					break;
				} else {
					isFound = 0;
				}
				ptr = ptr->next;
				location++;
			}

		}

		if(isFound != 1) {
			cout << "The item wasn't found." << endl;
		}

	}
}
```

## Links
[Source codes of circular doubly linked list](https://github.com/Jalever/Data-Structure-and-Algorithm/blob/master/Data%20Structure/Linked%20List/Circular%20Doubly%20Linked%20List.cpp)
