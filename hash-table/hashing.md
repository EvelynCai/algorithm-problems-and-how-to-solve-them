---
description: Hash Table
---

# Hashing

### WHAT

An algorithm to generate a numeric representation of an object.

### WHY

To search in constant time: 

if we know the index of an element in array, we could access it in O\(1\) time.

### HOW

* design tradeoff: collision VS space waste
* collision resolution
  * open addressing \(i.e. looking for an open index instead\)
    * linear probing
      * find the next opening/empty cell linearly 
      * step size of probing= 1/time, e.g. + 1, + 1, + 1, ...
      * risk: primary cluster
      * solution: re-hashing \(load factor &gt; 2/3\)
    * quadratic probing
      * step size of probing= n ^ 2/time , e.g. + 1, + 4, + 9, ...
      * risk: secondary clustering
      * cause: fixed interval of probing
    * double hashing
      * use 2 hash functions:
        * hash values
        * step size of probing= 1 + \(k % \(m - 2\)\)
  * closed addressing
    * separate chaining
* performance depends. But if load factor is expected to be high, consider separate chaining at first.

