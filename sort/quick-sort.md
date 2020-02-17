---
description: Sort
---

# Quick Sort

## 1. WHAT

### 1.1 Overview

Merge sort is an algorithm that sorts an array in a giving order \(mostly ascending\) by:

* splitting the input into 2 halves 
  * as middle as possible
* mergeSorting the 2 halves respectively...until there is ONLY one element in the splitted part
* merging the sorted 2 halves into one 
  * compare from the top of each half
  * select the smaller one \(for ascending\) 
  * add it to the final result and take its next element for future comparison

![Illustration - Merge Sort](../.gitbook/assets/screen-shot-2020-02-11-at-10.07.24-pm.png)

### 1.2 Time Complexity

O\(nlogn\)

* split: 
  * since elements in arrays are randomly accessible, we could find the mid index in O\(1\) 
  * since there are n elements in arrays, binary splitting takes log\(n\) times to make splitted part contain ONLY 1 element 
  * in general, splitting takes O\(logn\) time
* merge:
  * to compare and sort splitted subarrays, we have to iterate all the elements of these subarrays -&gt; in total, each round takes O\(n\)
  * it takes log\(n\) rounds merging from one element in each subarray to an entirely sorted array
  * in total, merging takes O\(nlogn\) time

### 1.3 Space Complexity

O\(n\)

* Breakpoint at recursion call, we use extra space for call stack to store element\#: n/2 + n/4 + n/8 + ... + 1 = O\(n\)

## 2. WHY

Merge sort is a stable, comparison-based sorting algorithm.

## 3. HOW

```text
public void quickSort(int[] nums) {
    if (nums == null || nums.length <= 1) {
        return;
    }
    
    helper(nums, 0, nums.length - 1);
}

private void helper(int[] nums, int left, int right) {
    if (left >= right) {
        return;
    }
    
    
    int pivot = nums[right];
    int pivotIndex = partition(nums, left, right, pivot);
    
    helper(nums, left, pivotIndex - 1);
    helper(nums, pivotIndex + 1, right);
}

private int partition(int[] nums, int left, int right, int pivot) {
    int start = left - 1;
    int end = right;
    while (start <= end) {
        while (nums[++start] < pivot);
        
        while (end > start && nums[--end] > pivot);
        
        if (start >= end) {
            break;
        } else {
            swap(nums, start, end);
        }
    }
    
    swap(nums, start, right);
    return start;
}

private void swap(int[] nums, int a, int b) {
    int tmp = nums[a];
    nums[a] = nums[b];
    nums[b] = tmp;
}
```

### 3.1 Sort Colors\[LeetCode 75\]

## 





