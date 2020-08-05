---
description: Stack
---

# Overview

Implement Queue with 2 Stacks

```text
public class MyQueue {
  Stack<Integer> s1;
  Stack<Integer> s2;
  public MyQueue() {
    s1 = new Stack<>();
    s2 = new Stack<>();
  }
  
  public Integer poll() {
    if (isEmpty()) {
      return null;
    }

    if (!s2.isEmpty()) {
      return s2.pop();
    }

    while (!s1.isEmpty()) {
      s2.push(s1.pop());
    }
    return s2.pop();
  }
  
  public void offer(int element) {
    s1.push(element);
  }
  
  public Integer peek() {
    if (isEmpty()) {
      return null;
    }
    
    if (!s2.isEmpty()) {
      return s2.peek();
    }

    while (!s1.isEmpty()) {
      s2.push(s1.pop());
    }
    return s2.peek();
  }
  
  public int size() {
    return s1.size() + s2.size();
  }
  
  public boolean isEmpty() {
    return s1.isEmpty() && s2.isEmpty();
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

