---
description: Sort
---

# Quick Sort

## 1. WHAT

### 1.1 Overview

Quick sort is an algorithm that sorts an array in a giving order \(mostly ascending\) by:

* partitioning the array with a selected pivot where
  * all the elements `< pivot` are on its left
  * all the elements `> pivot` are on its right 
* swapping the pivot to the middle
* quickSorting the left part until it contains 1 element ONLY
* quickSorting the right part until it contains 1 element ONLY

### 1.2 Time Complexity

Time complexity depends on how to pick the `pivot`:

* On average, we could assume the `pivot` always divide the array into 2 parts with similar amount of elements. So we recurse `logn` rounds in total, while every round we have to iterate all of the n elements to partition.
* In the worst case, we always pick the largest/smallest element `pivot`, which makes all other elements add on one side. So we recurse `n` times in total, while every round we have to iterate all of the n elements to partition.
* Average: O\(nlogn\)
* Worst: O\(n ^ 2\)

### 1.3 Space Complexity

O\(1\)

No extra space is used because we are mainly swapping elements within input array.

## 2. WHY

Quick sort is a unstable, comparison-based sorting algorithm.

## 3. HOW

### 3.1 Partition By RightMost Index

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

### 3.2 Partition By Mid Index of the Array

```text
private void partitionByMid(int[] nums, int left, int right) {
}
```

### [3.3 Sort Colors\[LeetCode 75\]](https://app.gitbook.com/@alittlebit/s/algorithm-problems-and-how-to-solve-them/array/75.-sort-colors)

## 





