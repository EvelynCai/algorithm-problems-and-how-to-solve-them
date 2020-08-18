---
description: Heap
---

# Determine If Array Is Min Heap

Determine if the given integer array is min heap.

```text
public boolean isMinHeap(int[] array) {
    if (array == null || array.length == 0) {
      return false;
    }

    return dfs(array, 0);
  }

private boolean dfs(int[] array, int i) {
    int left = 2 * i + 1;
    int right = left + 1;
    if (left < array.length && array[i] > array[left]) {
      return false;
    }
    if (right < array.length && array[i] > array[right]) {
      return false;
    }

    if (right < array.length) {
      return dfs(array, left) && dfs(array, right);
    } else if (left < array.length) {
      return dfs(array, left);
    } else {
      return true;
    }
}
```

