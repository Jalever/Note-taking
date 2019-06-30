---
layout: post
title: (DS Tree)B+ Tree
subtitle: Data Structure Tree学习笔记系列
date: 2019-06-30
author: Jalever
header-img: img/post-bg-star.jpg
catalog: true
tags:
  - Data Structure
---

- [Overview](#overview)
- [Advantages of B+ Tree](#advantages-of-b+-Tree)
- [B Tree compare to B+ Tree](#b-tree-compare-to-b+-tree)
- [Operations](#operations)
    - [Insertion](#insertion)
    - [Deletion](#deletion)

## Overview
B+ Tree is an extension of B Tree which allows efficient insertion, deletion and search operations.

In B Tree, Keys and records both can be stored in the internal as well as leaf nodes. Whereas, in B+ tree, records (data) can only be stored on the leaf nodes while internal nodes can only store the key values.

<ins>The leaf nodes of a B+ tree are linked together in the form of a singly linked lists to make the search queries more efficient.</ins>

B+ Tree are used to store the large amount of data which can not be stored in the main memory. Due to the fact that, size of main memory is always limited, the internal nodes (keys to access records) of the B+ tree are stored in the main memory whereas, leaf nodes are stored in the secondary memory.

The internal nodes of B+ tree are often called `index nodes`. A B+ tree of order 3 is shown in the following figure.

![Z1QCZV.png](https://s2.ax1x.com/2019/06/30/Z1QCZV.png)

## Advantages of B+ Tree
1. Records can be fetched in equal number of disk accesses.
2. Height of the tree remains balanced and less as compare to B tree.
3. We can access the data stored in a B+ tree sequentially as well as directly.
4. Keys are used for indexing.
5. Faster search queries as the data is stored only on the leaf nodes

## B Tree compare to B+ Tree
<table>
    <thead>
        <tr>
            <td></td>
            <td>B Tree</td>
            <td>B+ Tree</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>Search keys can not be repeatedly stored.</td>
            <td>Redundant search keys can be present.</td>
        </tr>
        <tr>
            <td>2</td>
            <td>Data can be stored in leaf nodes as well as internal nodes</td>
            <td>Data can only be stored on the leaf nodes.</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Searching for some data is a slower process since data can be found on internal nodes as well as on the leaf nodes.</td>
            <td>Searching is comparatively faster as data can only be found on the leaf nodes.</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Deletion of internal nodes are so complicated and time consuming.</td>
            <td>Deletion will never be a complexed process since element will always be deleted from the leaf nodes.</td>
        </tr>
        <tr>
            <td>5</td>
            <td>Leaf nodes can not be linked together.</td>
            <td>Leaf nodes are linked together to make the search operations more efficient.</td>
        </tr>
    </tbody>
</table>

## Operations
#### Insertion
1. Insert the new node as a leaf node
2. If the leaf doesn't have required space, split the node and copy the middle node to the next index node.
3. If the index node doesn't have required space, split the node and copy the middle element to the next index page.

For Example:

Insert the value 195 into the B+ tree of order 5 shown in the following figure.
![Z1l37V.png](https://s2.ax1x.com/2019/06/30/Z1l37V.png)

195 will be inserted in the right sub-tree of 120 after 190. Insert it at the desired position.
![Z1lNp4.png](https://s2.ax1x.com/2019/06/30/Z1lNp4.png)

The node contains greater than the maximum number of elements i.e. 4, therefore split it and place the median node up to the parent.
![Z1lU1J.png](https://s2.ax1x.com/2019/06/30/Z1lU1J.png)

Now, the index node contains 6 children and 5 keys which violates the B+ tree properties, therefore we need to split it, shown as follows.
![Z1lB0x.png](https://s2.ax1x.com/2019/06/30/Z1lB0x.png)

#### Deletion
1. Delete the key and data from the leaves.
2. if the leaf node contains less than minimum number of elements, merge down the node with its sibling and delete the key in between them.
3. if the index node contains less than minimum number of elements, merge the node with the sibling and move down the key in between them.

For Example:

Delete the key 200 from the B+ Tree shown in the following figure.
![Z1lvBq.png](https://s2.ax1x.com/2019/06/30/Z1lvBq.png)

200 is present in the right sub-tree of 190, after 195. delete it.
![Z11pNT.png](https://s2.ax1x.com/2019/06/30/Z11pNT.png)

Merge the two nodes by using 195, 190, 154 and 129.
![Z11i34.png](https://s2.ax1x.com/2019/06/30/Z11i34.png)

Now, element 120 is the single element present in the node which is violating the B+ Tree properties. Therefore, we need to merge it by using 60, 78, 108 and 120.

Now, the height of B+ tree will be decreased by 1.
![Z11FgJ.png](https://s2.ax1x.com/2019/06/30/Z11FgJ.png)
