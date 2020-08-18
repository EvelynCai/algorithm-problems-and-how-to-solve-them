---
description: heap
---

# Heap Offer Operation

Given a binary min heap in array format. The last cell of the array is not used.

Now offer a new element into the heap.

**Assumptions:**

* The given array is not null and has length &gt;= 1

**Examples:**

array = {2, 3, 4, 0}, offer\(1\) --&gt; {1, 2, 4, 3}

```text
public int[] offerHeap(int[] array, int ele) {
    int len = array.length - 1;
    array[len] = ele;

    siftUp(array, len);
    return array;
  }

  private void siftUp(int[] array, int i) {
    int parent = (i - 1) / 2;
    if (parent >= 0 && array[parent] > array[i]) {
      swap(array, parent, i);
      siftUp(array, parent);
    }
  }

  private void swap(int[] array, int a, int b) {
    int tmp = array[a];
    array[a] = array[b];
    array[b] = tmp;
  }
```

