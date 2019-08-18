---
layout: post
title: (DS Queue)Circular Queue
subtitle: Data Structure Queue
date: 2019-07-02
author: Jalever
header-img: img/home-bg2.jpg
catalog: true
tags:
  - Data Structure
---
- [Problem of Linear Queue](#problem-of-linear-queue)
- [Circular Queue](#circular-queue)
- [Time Complexity](#time-complexity)
- [Operation](#operation)
    - [Insertion](#insertion)
    - [Deletion](#deletion)
    - [Display](#display)
- [Implementation in CPP](#implementation-in-cpp)


## Problem of Linear Queue
Deletions and insertions can only be performed at front and rear end respectively, as far as linear queue is concerned.

Consider the queue shown in the following figure.

![ZJCi26.png](https://s2.ax1x.com/2019/07/02/ZJCi26.png)

The Queue shown in above figure is completely filled and there can't be inserted any more element due to the condition `rear == max - 1` becomes true.

However, if we delete 2 elements at the front of the queue, we still can not insert any element since the condition `rear = max -1` still holds.

This is the main problem with the linear queue, although we have space available in the array, but we can not insert any more element in the queue. This is simply the memory wastage and we need to overcome this problem.

![ZJCmad.png](https://s2.ax1x.com/2019/07/02/ZJCmad.png)

## Circular Queue
One of the solution of this problem is <ins>Circular Queue</ins>. In the circular queue, the first index comes right after the last index. You can think of a circular queue as shown in the following figure.
![ZJCwR0.png](https://s2.ax1x.com/2019/07/02/ZJCwR0.png)

Circular queue will be full when `front = -1` and `rear = max-1`. Implementation of circular queue is similar to that of a linear queue. Only the logic part that is implemented in the case of insertion and deletion is different from that in a linear queue.
![ZJPmOU.png](https://s2.ax1x.com/2019/07/02/ZJPmOU.png)

## Time Complexity
<table>
    <thead>
        <tr>
            <td>Front</td>
            <td>Rear</td>
            <td>Enqueue()</td>
            <td>Dequeue()</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>O(1)</td>
            <td>O(1)</td>
            <td>O(1)</td>
            <td>O(1)</td>
        </tr>
    </tbody>
</table>

## Operation
#### Insertion
There are three scenario of inserting an element in a queue.

1. If `(rear + 1)%maxsize = front`, the queue is full. In that case, overflow occurs and therefore, insertion can not be performed in the queue.
2. If `rear != max - 1`, then rear will be incremented to the `mod(maxsize)` and the new value will be inserted at the rear end of the queue.
3. If `front != 0` and `rear = max - 1`, then it means that queue is not full therefore, set the value of rear to 0 and insert the new element there.
![mmD7tA.png](https://s2.ax1x.com/2019/08/16/mmD7tA.png)

#### Deletion
To delete an element from the circular queue, we must check for the three following conditions.

1. If `front = -1`, then there are no elements in the queue and therefore this will be the case of an underflow condition.
2. If there is only one element in the queue, in this case, the condition `rear = front` holds and therefore, both are set to -1 and the queue is deleted completely.
3. If `front = max -1` then, the value is deleted from the front and the value of front is set to 0.
4. Otherwise, the value of front is incremented by 1 and then delete the element at the front end.
![mmrgEQ.png](https://s2.ax1x.com/2019/08/16/mmrgEQ.png)

#### Display
![ZJAiuV.png](https://s2.ax1x.com/2019/07/02/ZJAiuV.png)
![mms8Gn.png](https://s2.ax1x.com/2019/08/16/mms8Gn.png)

## Implementation in CPP
```cpp
#include <iostream>

#define MAXSIZE 5

using namespace std;

int front = -1, rear = -1;
int Queue[MAXSIZE];

void Insertion() {
	int value;
	cout << "Please Enter a value: ";
	cin >> value;

	if((rear+1)%MAXSIZE == front) {
		cout << "OVERFLOW..." << endl;
		return;
	} else if(front == -1 && rear == -1) {
		front = 0;
		rear = 0;
	} else if(rear == MAXSIZE-1 && front != 0) {
		rear = 0;
	} else {
		rear = (rear+1)%MAXSIZE;
	}

	Queue[rear] = value;

	cout << "\nInsert a Value Successfully!" << endl;
}

void Deletion() {
	if(front == -1 && rear == -1) {
		cout << "UNDERFLOW..." << endl;
		return;
	} else if(front == rear) {
		front = -1;
		rear = -1;
	} else if(front == MAXSIZE-1) {
		front = 0;
	} else {
		front = front + 1;
	}
}


void Display() {

	int i;
	   if(front == -1) {
		   printf("\nCircular Queue is Empty!!!\n");
	   } else {
	      i = front;

	      cout << "\nCircular Queue Elements are : \n";
	      if(front <= rear){
	    	  while(i <= rear)
	    		  cout << Queue[i++] << " ";
	      } else {
	    	  while(i <= MAXSIZE - 1){
	    		  cout << Queue[i++] << " ";
	    	  }

	    	  i = 0;

	    	  while(i <= rear) {
	    		  cout << Queue[i++] << " ";
	    	  }
	      }
	   }
}

int main() {

	int choice;

	while(choice != 4) {
		cout << "1.Insert an element" << endl;
		cout << "2.Delete an element" << endl;
		cout << "3.Display the queue" << endl;
		cout << "4.Exit" << endl;

		cout << "Please enter a choice: ";
		cin >> choice;

		switch(choice) {
			case 1: {
				Insertion();
				break;
			}
			case 2: {
				Deletion();
				break;
			}
			case 3: {
				Display();
				break;
			}
			case 4: {
				break;
			}
			default:{
				cout << "Please Enter a valid Value!" << endl;
			}
		}


	}

	return 0;
}

```
