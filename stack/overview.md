---
description: Stack
---

# Overview

### WHAT

#### \[Concept\]

A logical concept. Stacks could be implemented with various data structures, e.g. LinkedList, ArrayDuque, etc.

#### \[Operations\]

* push\(\): add an element at the top of stacks, O\(1\)
* pop\(\): remove the stack top and return its value, O\(1\)
* peek\(\): return the value of stack top, O\(1\)
* isEmpty\(\): return if the stack is empty

### WHY

* Last In First Out
* Manipulate the orders:
  * Transfer the elements from stack1 to stack2, the element order in stack2 is reversed;
  * Then transfer the elements back to stack1, the element order in stack1 == stack1 original order 

### HOW

Implement Deque with 3 Stacks 

```text
public class Solution {
  Stack<Integer> s1;
  Stack<Integer> s2;
  Stack<Integer> s3;

  public Solution() {
    s1 = new Stack<>();
    s2 = new Stack<>();
    s3 = new Stack<>();
  }
  
  public void offerFirst(int element) {
    s1.push(element);
  }
  
  public void offerLast(int element) {
    s2.push(element);
  }
  
  public Integer pollFirst() {
    if (isEmpty()) {
      return null;
    }

    if (size() == 1 && s1.isEmpty()) {
      return pollLast();
    }
    
    if (s1.isEmpty()) {
      shuffle(s2, s1);
    }
    return s1.pop();
  }
  
  public Integer pollLast() {
    if (isEmpty()) {
      return null;
    }

    if (size() == 1 && s2.isEmpty()) {
      return pollFirst();
    }

    if (s2.isEmpty()) {
      shuffle(s1, s2);
    }
    return s2.pop();
  }
  
  public Integer peekFirst() {
    if (isEmpty()) {
      return null;
    }

    if (size() == 1 && s1.isEmpty()) {
      return peekLast();
    }

    if (s1.isEmpty()) {
      shuffle(s2, s1);
    }
    return s1.peek();
  }
  
  public Integer peekLast() {
    if (isEmpty()) {
      return null;
    }

    if (size() == 1 && s2.isEmpty()) {
      return peekFirst();
    }

    if (s2.isEmpty()) {
      shuffle(s1, s2);
    }
    return s2.peek();
  }
  
  public int size() {
    return s1.size() + s2.size();
  }
  
  public boolean isEmpty() {
    return size() == 0;
  }

  private void shuffle(Stack<Integer> out, Stack<Integer> in) {
    int goal = size() / 2;
    while (out.size() < goal) {
      s3.push(out.pop());
    }

    while (!out.isEmpty()) {
      in.push(out.pop());
    }

    while (!s3.isEmpty()) {
      out.push(s3.pop());
    }
  }
}
```

Implement Merge Sort with 3 Stacks

Implement Selection Sort with 2 Stacks

Implement min\(\) with 2 Stacks

```text
public class Solution {
  class Pair {
    int minValue;
    int index;
    Pair(int minValue, int index) {
      this.minValue = minValue;
      this.index = index;
    }
  }

  Stack<Integer> nums;
  Stack<Pair> mins;
  public Solution() {
    nums = new Stack<>();
    mins = new Stack<>();
  }
  
  public int pop() {
    if (nums.isEmpty()) {
      return -1;
    }

    int tmp = nums.peek();
    Pair p = mins.peek();
    if (tmp == p.minValue && nums.size() <= p.index) {
      mins.pop();
    }
    return nums.pop();
  }
  
  public void push(int element) {
    nums.push(element);

    if (mins.isEmpty() || element < min()) {
      mins.push(new Pair(element, nums.size()));
    }
  }
  
  public int top() {
    if (nums.isEmpty()) {
      return -1;
    }

    return nums.peek();
  }
  
  public int min() {
    if (nums.isEmpty()) {
      return -1;
    }
    
    Pair p = mins.peek();
    return p.minValue;
  }
}
```

