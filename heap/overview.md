---
description: Heap
---

# Overview

### WHAT

A binary tree which is:

* almost complete: 
  * every level has the max amount of nodes, except the last/leave level
  * the leave level is filled in from left to right \(no bubble\)
* partially ordered:
  * the root is max/min node
  * for each node, its children have smaller/larger keys \(than its own key\)

### WHY

Common operations

N.B. n = total amount of tree nodes, logn = tree height because it's self-balanced

* insert: O\(logn\) 
  * insert the new element at the last position \(complete\) - O\(1\)
  * percolate it up \(until the heap order is restored\) - O\(logn\)
* pop/delete top: O\(logn\) 
  * remove the top/first element - O\(1\)
  * put the element at the last position at the top \(complete\) - O\(1\)
  * percolating it down \(until the heap order is restored\) - O\(logn\)
* peek/get top: O\(1\)
* update: O\(logn\)
* heapify/buildHeap: O\(n\)
  * use "percolate down" method because:
    * 1 node\(top\) needs to percolate down logn times
    * n/2 nodes\(leaves\) don't need to percolate down 
    * in total, `0 * n/2 + 1 * n/4 + 2 * n/8 +  ... + logn * 1`
    * the result upper bound is O\(n\): [https://stackoverflow.com/questions/9755721/how-can-building-a-heap-be-on-time-complexity](https://stackoverflow.com/questions/9755721/how-can-building-a-heap-be-on-time-complexity)

![get the infinite value with Taylor Series](../.gitbook/assets/image%20%282%29.png)

* [heapSort](https://app.gitbook.com/@alittlebit/s/algorithm-problems-and-how-to-solve-them/sort/heapsort): O\(nlogn\)
  * heapify: O\(n\)
  * pop up the top \* n times: O\(n \* logn\)

### HOW

Binary tree is the conceptual view of Heap, when it comes to implementation:

Array

* current: index = i
* parent: index = \(i - 1\) / 2
* leftChild: index = 2 \* i + 1
* rightChild: index = 2 \* i + 2 = leftChild + 1

PriorityQueue

* a class of Java Collections Framework 
* min-heap by default
* major APIs
  * add\(object\) / offer\(object\): O\(logn\)
  * poll\(\): O\(logn\)
  * peek\(\): O\(1\)
  * remove\(object\): O\(n\)
    * search/find: O\(n\)
    * remove and percolate up: O\(logn\)

### WHEN

* 215. Kth largest element in an array

