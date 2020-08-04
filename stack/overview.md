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

