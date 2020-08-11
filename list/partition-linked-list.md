---
description: LinkedList
---

# 86. Partition List

### 1. [Description](https://leetcode.com/problems/partition-list/)

Given a linked list and a value _x_, partition it such that all nodes less than _x_ come before nodes greater than or equal to _x_.

You should preserve the original relative order of the nodes in each of the two partitions.

**Example:**

```text
Input: head = 1->4->3->2->5->2, x = 3
Output: 1->2->2->4->3->5
```

### 2. Solution

To partition the list based on the target, we want to split the entire list into 2 halves:

* smaller elements sub-list
* larger \(and equal to\) elements sub-list

So we need to iterate the list from start to end:

* if the current element we are looking at &lt; target, append it to the smaller elements sub-list
* if the current element we are looking at &gt;= target, append it to the larger elements sub-list

Finally, we just need to append the head of larger element sub-list to the tail of smaller element sub-list.

N.B. remember to break the `next` of larger element sub-list in case of cycles.

{% hint style="info" %}
**Complexity:**

* Time: O\(n\)  

where n represents the amount of list nodes because of the iteration.

* Space: O\(1\) 

since we use constant extra space during the iteration.
{% endhint %}

### 3. JAVA Implementation

```text
public ListNode partition(ListNode head, int target) {
    if (head == null) {
      return head;
    }

    ListNode dummySmall = new ListNode(-1);
    ListNode tailSmall = dummySmall;
    ListNode dummyLarge = new ListNode(-1);
    ListNode tailLarge = dummyLarge;
    while (head != null) {
      if (head.value < target) {
        tailSmall.next = head;
        tailSmall = tailSmall.next;
      } else {
        tailLarge.next = head;
        tailLarge = tailLarge.next;
      }
      head = head.next;
    }

    tailLarge.next = null;
    tailSmall.next = dummyLarge.next;
    return dummySmall.next;
}
```

### 4. Comments

A combination of:

* merge two lists

