---
description: DFS
---

# 46. Permutation

### 1. [Problem](https://leetcode.com/problems/permutations/)

Given a collection of **distinct** integers, return all possible permutations.

**Example:**

```text
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

### 2. Solution

Depth First Search

                                                                             \[1, 2, 3\]

                                                            /                   \|                    \

Level 0 \(position 0?\)      \[1 \| 2, 3\]             \[2 \| 1, 3\]           \[3 \| 2, 1\]

                                             /        \               /       \                   /          \

Level 1 \(position 1?\) \[1, 2 \| 3\] \[1, 3 \| 2\] \[2, 1 \| 3\] \[2, 3 \| 1\]   \[3, 2 \| 1\] \[3, 1 \| 2\]

                                           \|              \|            \|               \|                \|              \|    

Level 2 \(position 2?\) \[1, 2, 3\]  \[1, 3, 2\]   \[2, 1, 3\]   \[2, 3, 1\]     \[3, 2, 1\]   \[3, 1, 2\]

The result should contain all the elements involved, so we could use `swap` 

* base case: only 1 element left to swap
* recursive rule: 
  * use an `index` to indicate the current level \(position in nums array\);
  * elements before `index`: fixed
  * elements after `index` : iterate and swap with `index`

{% hint style="info" %}
**Time Complexity:** O\(n!\) where n represents the length of input array

because at level/position 0, we have n options to swap;

                 at level/position 1, we have \(n - 1\) options to swap;

                    ......

                  at level/position \(n - 1\), we have 1 option ONLY.

so in total, it's n \* \(n - 1\) \* \(n - 2\) \* ... \* 2 \* 1 = n!

**Space Complexity:** O\(n\) 

because the call stack/recursion tree height is n.
{% endhint %}

### 3. JAVA Implementation

```text
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        return res;
    }
    
    dfs(res, nums, 0);
    return res;
}

private void dfs(List<List<Integer>> res, 
                 int[] nums, 
                 int index) {
    if (index == nums.length - 1) {
        // convert int[] to List<Integer>
        res.add(Arrays.stream(nums).boxed().collect(Collectors.toList()));
        return;
    }
    
    for (int i = index; i < nums.length; i++) {
        swap(nums, i, index);
        dfs(res, nums, index + 1);
        swap(nums, i, index);
    }
}

private void swap(int[] nums, int a, int b) {
    int tmp = nums[a];
    nums[a] = nums[b];
    nums[b] = tmp;
}
```

### 4. Comment

4.1 Convert int\[\] to List&lt;Integer&gt; :

`Arrays.stream(array).boxed().collect(Collectors.toList());`



