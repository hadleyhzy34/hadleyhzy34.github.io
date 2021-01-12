---
layout: post
title: Linked List
key: 20201026
tags:
  - C++
  - data structure and algorithm
  - Linked List
---

## 1.Linked List Definition
```c++
//Tree Declaration
struct Node
{
    int val;
    Node *next;
    Node():val(0),next(nullptr){};
    Node(x):val(x),next(nullptr){};
    Node(x,Node* node):val(x),next(node)(); 
};
//Tree Initializaiton with default value zero
Node *node=new Node();
```
<!--more-->
## Reorder Linked List
### inplace
* 328 Odd Even Linked List([Q](https://leetcode.com/problems/odd-even-linked-list/):[A]())(two node pointers through iteration)

## Build Linked List
### Linked List from right to left
* 369 Plus One Linked List([Q](https://leetcode.com/problems/plus-one-linked-list/):[A]())


## List
Lists are sequence containers that allow non-continguous memory allocation. As compared to vector, list has slow traversal, but once a position has been found, insertion and deletion are quick. 

List Initialization and Traversal
```c++
//initialize list from specified elements
std::list<char> string{'A','B','C'};
//copy constructor
std::list<char> chars(string);
//initialize list from array
char array[]={'A','B','C'};
std::list<char> charss(std::begin(array),std::end(array));
//initialize specified size by specified element
std::list<char> charsss(size,'A');

//traversal list1
for(char c:chars)

//traversal list2
for(auto it=chars.begin();it!=chars.end();it++)
```

List functions
* front()
* back()
* push_front()
* push_back()
* pop_front()
* pop_back()
* erase

`list_name.erase(iterator position)` or `list_name.erase(iterator first, iterator last)`

* 146 LRU Cache([Q](https://leetcode.com/problems/lru-cache/):[A]())(hashtable,list)
