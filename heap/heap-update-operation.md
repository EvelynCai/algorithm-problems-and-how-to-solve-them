---
description: Heap
---

# Heap Update Operation

Given a binary min heap in array format. Update the element at a specified index.

**Assumptions:**

* The given array is not null or empty.
* The specified index is guaranteed to be within the range.

**Examples:**

array = {1, 2, 3, 4}, update the element at index 1 to 5, the array becomes {1, 4, 3, 5}

```text
public int[] updateHeap(int[] array, int index, int ele) {
    array[index] = ele;
    siftUp(array, index);
    siftDown(array, index);
    return array;
}

private void siftUp(int[] array, int i) {
    int parent = (i - 1) / 2;
    if (parent >= 0 && array[parent] > array[i]) {
      swap(array, i, parent);
      siftUp(array, parent);
    }
}

private void siftDown(int[] array, int i) {
    int left = 2 * i + 1;
    int right = left + 1;
    int smallest = i;
    if (left < array.length && array[left] < array[smallest]) {
      smallest = left;
    }
    if (right < array.length && array[right] < array[smallest]) {
      smallest = right;
    }
    if (smallest != i) {
      swap(array, i, smallest);
      siftDown(array, smallest);
    }
}

private void swap(int[] array, int a, int b) {
    int tmp = array[a];
    array[a] = array[b];
    array[b] = tmp;
}
```

