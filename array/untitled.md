---
description: voting
---

# 229. Majority Element II

### 1. [Description](https://leetcode.com/problems/majority-element-ii/description/)

Given an integer array of size n, find all elements that appear more than `⌊ n/3 ⌋` times.

**Note:** The algorithm should run in linear time and in O\(1\) space.

**Example 1:**

```text
Input: [3,2,3]
Output: [3]
```

**Example 2:**

```text
Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```



### 2. Solution

Similar to 169. Majority Element, the only difference is the candidate frequency is more than n / 3 times. So at most, there could be two candidates.

Likewise, the hashtable and sorting solution can be migrated here. However, there is not modifications in Boyer-Moore Majority Vote Algorithm due to the variance of candidates.

This time, the vote algorithm requires to maintain 2 candidates and their frequencies respectively:

* start with candidate1 = nums\[0\], freq1 = 1
* set the other candidate2 = nums\[0\], freq2 = 0 
  * set candidate2 = nums\[0\] because there might be cases like \[6, 6, 6, 6, 5\] where it's hard to get the second distinct number
  * set freq2 = 0 in order to assign the second distinct number to candidate2
* iterate the input array and compare current element to candidate
  * if candidate1 = current element, freq1++
  * else if candidate2 = current element, freq2++
  * else if freq1 == 0, i.e. candidate1's frequency is not affordable to compete one more round -&gt; update candidate1 with current element & freq1 = 1
  * else if freq2 == 0, i.e. candidate2's frequency is not affordable to compete one more round -&gt; update candidate2 with current element & freq2 = 1
  * otherwise,  both candidates  can afford another round of compete -&gt; freq1-- & freq2--
* 2nd pass over the input array and check candidate's actual frequency
* return candidate\(s\) whose real frequency &gt; n / 3

{% hint style="info" %}
**Complexity:**

* Time: O\(n\)  

where n represents the length of input array. In essence, it requires 2 pass over the entire input array.

* Space: O\(1\) 

because of constant extra space taken by the counters and candidates.
{% endhint %}



### 3. JAVA Implementation

```text
public List<Integer> majorityElement(int[] nums) {
        List<Integer> res = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            return res;
        }
        
        int vote1 = nums[0];
        int count1 = 1;
        int vote2 = nums[0];
        int count2 = 0;
        for (int i = 1; i < nums.length; i++) {
            if (vote1 == nums[i]) {
                count1++;
            } else if (vote2 == nums[i]) {
                count2++;
            } else if (count1 == 0) {
                vote1 = nums[i];
                count1 = 1;
            } else if (count2 == 0) {
                vote2 = nums[i];
                count2 = 1;
            } else {
                count1--;
                count2--;
            }
        }
        
        count1 = 0;
        count2 = 0;
        for (int n: nums) {
            if (n == vote1) {
                count1++;
            } else if (n == vote2) {
                count2++;
            }
        }
        
        if (count1 > nums.length / 3) {
            res.add(vote1);
        }
        
        if (count2 > nums.length / 3) {
            res.add(vote2);
        }
        
        return res;
}
```



### 4. Analysis

* 169. Majority Elements I
* 1150. Check if Number if Majority Element in a Sorted Array
* what if majority elements means the elements which appears more than n / k?

