---
description: LinkedList
---

# Overview

### WHAT

#### Concept

#### Mistakes

1. **Check `NULL` before dereference a node to avoid Null Pointer Exception**, e.g.

```text
if (node != null) {
    System.out.println(node.value);
    node = node.next;
}
```

    2. **Don't lose track of the `head` pointer,**

e.g. Reverse the following Linked List:

Node1 -&gt; Node2 -&gt; Node3 -&gt; Node4 -&gt; NULL

Node1 &lt;- Node2      Node3 -&gt; Node4 -&gt; NULL

lose the head pointer to continue with Node3

    3. **Keep track of  `tail` pointer could make appending easier**

    4. **Remember to avoid cycles!**

e.g. break the previous `next` pointer after re-organizing, e.g. partition linked list

### WHY

Time Complexity

### WHEN

| Category | Problem | Notes |
| :--- | :--- | :--- |
| Reverse | 206. Reverse Linked List |  |
|  | 92. Reverse Linked List II |  |
|  | 25. Reverse Nodes in k-Group |  |
|  | 24. Swap Nodes in Pairs |  |
|  | 61. Rotate List | Rotate |
| Removal | 83. Remove Duplicates from Sorted List |  |
|  | 82. Remove Duplicates from Sorted List II |  |
|  | 203. Remove Linked List Elements |  |
|  | 19. Remove Nth Node From End of List | One-pass |
| Merge | 21. Merge Two Sorted Lists |  |
|  | 141. Linked List Cycle |  |
|  | 142. Linked List Cycle II |  |
|  | 328. Odd Even Linked List |  |
| Sort | 147. Insertion Sort List |  |
|  | 148. Sort List | Merge Sort |
| Intersection | 160. Intersection of Two Linked Lists |  |
| Copy | 138. Copy List With Random Pointer |  |
| Others | 234. Palindrome Linked List |  |

