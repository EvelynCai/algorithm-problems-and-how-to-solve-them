---
description: sort
---

# HeapSort

### WHAT

An unstable sorting algorithm based on comparison.

Principle:

Similar to Selection Sort, but use heap to popup the min/max instead of for loop.



### HOW

```text
public int[] heapsort(int[] array) {
    if (array == null || array.length == 0) {
      return array;
    }

    PriorityQueue<Integer> pq = new PriorityQueue<>();
    for (int n: array) {
      pq.offer(n);
    }

    for (int i = 0; i < array.length; i++) {
      array[i] = pq.poll();
    }

    return array;
}
```

{% hint style="info" %}
Time: O\(nlogn\)

where n represents the size of input array

dominates by finding the min/max with the PriorityQueue to fill in n positions

* polling current min/max from PriorityQueue: O\(logn\)
* iterate to fill in the input array: O\(n\)
* overall: O\(nlogn\)

Space: O\(1\)

 in-place
{% endhint %}

