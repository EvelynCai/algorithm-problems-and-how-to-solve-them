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

Common operations: 

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
    * the result upper bound is O\(n\):

![get the infinite value with Taylor Series](../.gitbook/assets/image%20%282%29.png)

* heapSort: O\(nlogn\)

### HOW

PriorityQueue

Time Complexity:

* heapify: O\(n\)
* insert
* 
