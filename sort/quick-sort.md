---
description: Sort
---

# Quick Sort

### WHAT

An unstable sorting algorithm based on comparison.

**Principle: Partition**

* selecting a pivot to partition the array so that
  * all the elements `< pivot` are on its left
  * all the elements `> pivot` are on its right 
* swapping the pivot to the exact position
* quickSorting the left part until it contains 1 element ONLY
* quickSorting the right part until it contains 1 element ONLY

### HOW

```text
public int[] quickSort(int[] array) {
    if (array == null || array.length <= 1) {
        return array;
    }
    
    partition(array, 0, array.length - 1);
    return array;
}

private void partition(int[] array, int left, int right) {
    if (left >= right) {
        return;
    }
    
    int start = left;
    int end = right;
    int pivot = array[left + (right - left) / 2];
    while (start <= end) {
        while (start <= end && array[start] < pivot) {
            start++;
        }
        
        while (start <= end && array[end] > pivot) {
            end--;
        }
        
        if (start <= end) {
            swap(array, start++, end--);
        }
    }
    
    partition(array, left, end);
    partition(array, start, right);
}

private void swap(int[] array, int left, int right) {
    int tmp = array[left];
    array[left] = array[right];
    array[right] = tmp;
}
```

{% hint style="info" %}
Time complexity: depends on how ideal  is the `pivot`

* Average: O\(nlogn\)

  we could assume the `pivot` always divide the array into 2 parts with similar amount of elements. So we recurse `logn` rounds in total, while every round we have to iterate all of the n elements to partition.

* Worst case: O\(n ^ 2\)

  we always pick the largest/smallest element `pivot`, which makes all other elements add on one side. So we recurse `n` times in total, while every round we have to iterate all of the n elements to partition.

Space complexity: O\(1\)

because no extra space is used because we are mainly swapping elements within input array.
{% endhint %}

### WHERE

Practice

* Partition By RightMost Index

```text
public void quickSort(int[] nums) {
    if (nums == null || nums.length <= 1) {
        return;
    }
    
    helper(nums, 0, nums.length - 1);
}

/**
* Helper function to recursively run quick sort on nums from index left to index right
* @param nums: input array
* @param left: start index of input array to run quick sort
* @param right: end index of input array to run quick sort
**/
private void helper(int[] nums, int left, int right) {
    if (left >= right) {
        return;
    }
    
    int pivot = nums[right]; // use nums[right] as pivot value
    int pivotIndex = partitionByRight(nums, left, right, pivot);
    // int pivotIndex = partitionByRight2(nums, left, right, pivot);
    
    helper(nums, left, pivotIndex - 1);
    helper(nums, pivotIndex + 1, right);
}

/**
* Partition the input array based on pivot originated from nums[right]
* @param nums: input array
* @param left: start index of input array to run partition
* @param right: end index of input array to run partition
* @param pivot: pivot value, i.e. nums[right]
**/
private int partitionByRight(int[] nums, int left, int right, int pivot) {
    int start = left - 1; // NOTE differs to partitionByRight2!
    int end = right;
    while (start <= end) {
        while (nums[++start] < pivot);
        
        while (end > start && nums[--end] > pivot);
        
        if (start >= end) {
            break;
        } else {
            swap(nums, start, end); // NOTE no increment if starts from (left - 1)
        }
    }
    
    swap(nums, start, right);
    return start;
}


private int partitionByRight2(int[] nums, int left, int right, int pivot) {
    int start = left;
    int end = right - 1;
    while (start <= end) {
        while (nums[start] < pivot) {
            start++;
        }
        
        while (end >= start && nums[end] > pivot) {
            end--;
        }
        
        if (start >= end) {
            break;
        } else {
            swap(nums, start++, end--); // NOTE increment if starts from left! otherwise TLE
        }
    }
    
    swap(nums, start, right);
    return start;
}

/**
* Swap the element of index a, b in input array nums
* @param nums: input array
* @param a: element index 1 to swap
* @param b: element index 2 to swap
**/
private void swap(int[] nums, int a, int b) {
    int tmp = nums[a];
    nums[a] = nums[b];
    nums[b] = tmp;
}
```

Extension

* Sort Colors\[LeetCode 75\]



