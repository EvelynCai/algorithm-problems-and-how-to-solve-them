---
description: 'Sort, Stack'
---

# Sort with 2 Stacks

### 1. Description

Given an array that is initially stored in one stack, sort it with one additional stacks \(total 2 stacks\).

After sorting the original stack should contain the sorted integers and from top to bottom the integers are sorted in ascending order.

**Assumptions:**

* The given stack is not null.
* There can be duplicated numbers in the give stack.

**Requirements:**

* No additional memory, time complexity = O\(n ^ 2\).

### JAVA Implementation

```text
public void sort(LinkedList<Integer> s1) {
    LinkedList<Integer> s2 = new LinkedList<Integer>(); // sorted results
    
    while (!s1.isEmpty()) {
        int tmp = s1.pop();
        while (!s2.isEmpty() && s2.peek() > tmp) {
            s1.push(s2.pop());
        }
        s2.push(tmp);
    }
    
    // transfer elements to s1
    while (!s2.isEmpty()) {
      s1.push(s2.pop());
    }
}
```

