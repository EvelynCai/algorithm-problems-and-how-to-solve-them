---
description: Sort
---

# Selection Sort

### WHAT

A in-place sorting sorting algorithm based on comparison.

**Nested Loops:**

* iterate `array` from 0 to array.length - 1 and use an `index` to denote the current index, so`array[index]` divides the `array` into 2 parts:
  * \[0, index\): already sorted
  * \[index, array.length - 1\]: unsorted
* for each `array[index]`
  * find the `minimum` in the unsorted part
  * swap the `minimum` with the current value, `array[index]` , i.e. put the minimum in unsorted part at the end of sorted part -&gt; go to the next element

### HOW

```text
public int[] selectionSort(int[] input) {
    if (input == null || input.length == 0) {
        return input;
    }
    
    for (int i = 0; i < input.length; i++) {
        int minIndex = i;
        for (int j = i + 1; j < input.length; j++) {
            if (input[j] < input[minIndex]) {
                minIndex = j;
            }
        }
        
        swap(input, i, minIndex);
    }
    
    return input;
}

private void swap(int[] input, int a, int b) {
    int tmp = input[a];
    input[a] = input[b];
    input[b] = tmp;
}
```

{% hint style="info" %}
**Time Complexity:** O\(n^2\) where n denotes the length of input array

because we use 2 for loops:

* outer loop: iterate each element in the input array \(use `i`\)
* inner loop: find the minimum between outer loop `i` and the end of input 

**Space Complexity**: O\(1\)

because it takes constant auxiliary space.
{% endhint %}

### WHY

* pros:
  * minimum possible swap operations
  * applicable when auxiliary space is limited
* cons:
  * quadratic time complexity

### WHERE

Practice:

* Leetcode 912: Sort an Array 

Extension: 

* use 3 stacks to implement selection sort
* use 2 stacks to implement selection sort

