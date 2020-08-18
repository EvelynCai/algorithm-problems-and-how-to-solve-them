---
description: Heap
---

# Heapify

Heapify an unsorted array to min heap.

```text
public int[] heapify(int[] array) {
    if (array == null || array.length == 0) {
        return array;
    }
    
    int start = array.length / 2 - 1;
    for (int i = start; i >= 0; i--) {
        siftDown(array, i);
    }
    
    return array;
}

private void siftDown(int[] array, int i) {
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    int smallest = i;
    if (left < array.length && array[left] < array[smallest]) {
        smallest = left;
    }
    if (right < array.length && array[right] < array[smallest]) {
        smallest = right;
    }
    
    if (smallest != i) {
        swap(array, smallest, i);
        siftDown(array, smallest);
    }
}

private void swap(int[] array, int a, int b) {
    int tmp = array[a];
    array[a] = array[b];
    array[b] = tmp;
}
```



