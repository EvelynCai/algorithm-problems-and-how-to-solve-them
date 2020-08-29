---
description: Hash Table
---

# Hashing

### WHAT

An algorithm to encode an object to be a \(unique\) index.

### WHY

To search in constant time.

Compress an object with a number/index.

### HOW

* design based on the tradeoff between collision VS space waste
* collision resolution
  * open addressing \(i.e. looking for an open index instead\)
    * linear probing
      * step = 1/time, e.g. + 1, + 1, + 1, ...
      * risk: cluster
      * solution: re-hashing \(load factor &gt; 2/3\)
    * quadratic probing
      * step = n ^ 2/time , e.g. + 1, + 4, + 9, ...
      * risk: secondary clustering
    * double hashing
      * step = 1 + \(k % \(m - 2\)\)
  * closed addressing
    * separate chaining
* performance depends. But if load factor is expected to be high, consider separate chaining at first.

