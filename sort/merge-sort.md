---
description: Sort
---

# Merge Sort

## WHAT

A stable sorting algorithm based on comparison.

**Divide and conquer:**

* splitting the input into 2 halves 
  * as middle as possible
* mergeSorting the 2 halves respectively...until there is ONLY one element in the splitted part
* merging the sorted 2 halves into one 
  * compare from the top of each half
  * select the smaller one \(for ascending\) 
  * add it to the final result and take its next element for future comparison

![Illustration - Merge Sort](../.gitbook/assets/screen-shot-2020-02-11-at-10.07.24-pm.png)

### HOW

```text
public int[] mergeSort(int[] array) {
    if (array == null || array.length < 2) {
        return array;
    }
    
    sort(array, 0, array.length - 1);
    return array;
}

private int[] sort(int[] array, int left, int right) {
    if (left >= right) {
        return new int[]{array[left]};
    }
    
    int mid = left + (right - left) / 2;
    int[] leftRes = sort(array, left, mid);
    int[] rightRes = sort(array, mid + 1, right);
    return merge(leftRes, rightRes);
}

private int[] merge(int[] arr1, int[] arr2) {
    int p1 = 0;
    int p2 = 0;
    int[] res = new int[arr1.length + arr2.length];
    int p = 0;
    while (p1 < arr1.length && p2 < arr2.length) {
        if (arr1[p1] < arr2[p2]) {
            res[p++] = arr1[p1++];
        } else {
            res[p++] = arr2[p2++];
        }
    }
    
    while (p1 < arr1.length) {
        res[p++] = arr1[p1++];
    }
    
    while (p2 < arr2.length) {
        res[p++] = arr2[p2++];
    }
    
    return res;
}
```

{% hint style="info" %}
**Time Complexity: O\(nlogn\)**

because

* split: 
  * since elements in arrays are randomly accessible, we could find the mid index in O\(1\) 
  * since there are n elements in arrays, binary splitting takes log\(n\) times to make splitted part contain ONLY 1 element 
  * in general, splitting takes O\(logn\) time
* merge:
  * to compare and sort splitted subarrays, we have to iterate all the elements of these subarrays -&gt; in total, each round takes O\(n\)
  * it takes log\(n\) rounds merging from one element in each subarray to an entirely sorted array
  * in total, merging takes O\(nlogn\) time

**Space Complexity: O\(n\)**

because breakpoint at recursion call, we use extra space for call stack to store element\#: n/2 + n/4 + n/8 + ... + 1 = O\(n\)
{% endhint %}

### WHERE

Assumption: ascending or descending?

Practice:

#### Merge Sorted Parts

* Merge 2 Sorted Arrays \[[LeetCode 88](https://app.gitbook.com/@alittlebit/s/algorithm-problems-and-how-to-solve-them/array/88.-merge-sorted-array) & LintCode 6\]
* Merge K Sorted Arrays \[LintCode 486\]
* Merge 2 Sorted Lists \[LeetCode 21 & LintCode 165\]
* Merge K Sorted Lists \[LintCode 104\]

#### MergeSort 

* MergeSort 2 arrays to 1 array \[LintCode 464\]
* MergeSort 2 arrays to 1 list \[LeetCode 912\]
* MergeSort 2 list to 1 list [\[LeetCode 148\]](https://app.gitbook.com/@alittlebit/s/algorithm-problems-and-how-to-solve-them/list/148.-sort-list)

#### Reorder Strings

* "a1b2c3d4e5" -&gt; "abcde12345"

substring\(startIndex, endIndex\); endIndex excluded.

*  "abcde12345" -&gt; "a1b2c3d4e5"



## 





