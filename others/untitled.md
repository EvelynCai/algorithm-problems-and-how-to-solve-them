# 349. Intersection of Two Arrays

### 1. [Problem](https://leetcode.com/problems/intersection-of-two-arrays/description/): 

Given two arrays, write a function to compute their intersection.

Example 1:

```text
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

Example 2:

```text
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```

**=&gt; Note:**

* Each element in the result must be unique.
* The result can be in any order.



### **2. Analysis:** 

Compute the intersection of 2 arrays.

#### **=&gt; Things to be clarified**

1. input : 2 unsorted integer arrays \(array1 and array2\)
2. output: 
   1. an integer array which contains all common elements in the 2 input arrays
   2. elements in outputs are unique \(appear once ONLY\)
   3. elements can be any order

**=&gt; In Essence**

to find the common elements in two unsorted arrays.

i.e. If an element exists in both arrays, it should be included in the result



### 3. Solution:

Iterate one of the arrays to check if any element is contained in the other array.

=&gt; To quickly check if an element is contained,

**Solution 1: Hash Table**

**Assumptions**

According to Problem Clarification 2.2 and 2.3, there is no requirement for the order and each element should appear once ONLY. So using Hash Table seems applicable.

**Steps**

1. add all the elements of one array, array1, to a HashSet, hashSet
2. iterate all the elements of the other array, array2, to check if any of its element is contained in hashSet
   1. if contained, that means the element exists both in array1 and in array2, which is in common -&gt; should be included in results
   2. if not, that means the element exists only in array2 -&gt; continue to check the next
3. return the result of common elements

**Complexity**

1. Time: O\(array1.length + array2.length\) 

{% hint style="info" %}
The fact is to iterate both arrays to check each element:

For one array\(say, array1\), we iterate all its elements to add them in a hashset. -&gt; O\(array1.length\)

For the other array\(e.g. array2\), we iterate all its element to check if it's contained in hashset of array1. -&gt; The check in hashtable is amortized to be O\(1\) -&gt; O\(1\) \* O\(array2.length\) = O\(array2.length\)

Total = O\(array1.length + array2.length\)
{% endhint %}

2. Space: O\(Math.min\(array1.length, array2.length\) \)

{% hint style="info" %}
Extra space is required for creating the hashset. -&gt; If we want to use less space, use hashset for the shorter array.
{% endhint %}

=&gt; To get rid of taking extra space, 

**Solution 2: Sort + 2 Pointers**

**Steps**

1. sort both arrays \(array1, array2\)
2. iterate the 2 arrays with 2 pointers\(pointer1, pointer2\) respectively:
   1. if what pointer1 points to is equal to what pointer2 points to -&gt; check if the common element is already contained in result -&gt; increase pointer1 and pointer2 by 1
      1. if so, forget about it
      2. if not, add it to result
   2. if what pointer1 pointers to a larger value, increase  pointer2 by 1 \(to let it points to something larger and hopefully be equal to pointer1's value\)
   3. if what pointer2 pointers to a larger value, increase  pointer1 by 1 \(similar to 2.2\)
3. terminate the loop when either of the pointers exceed its boundary, which means it's impossible to find anything in common from then on

**Complexity**

1. Time: O\(nlogn\) if n = Math.max\(array1.length, array2.length\)

{% hint style="info" %}
Built-in sort is based on comparison, which at best takes O\(nlogn\)

Iterate 2 arrays simultaneously and terminate when one of them hits the end 
{% endhint %}

  2. Space: O\(1\) 

{% hint style="info" %}
 2 pointers in need, which takes constant extra space
{% endhint %}

### 

### [4. JAVA Implementation:](https://leetcode.com/problems/generate-parentheses/discuss/331278/Java-DFS-solution-and-how-to-come-up-with-it)

```text
public int[] intersection(int[] nums1, int[] nums2) {
    // solution 1: Hash Table
    if (nums1 == null || nums2 == null) {
        return new int[]{};
    }

    Set<Integer> set = new HashSet<>();
    for (int n: nums1) {
        set.add(n);
    }
    
    int[] res = new int[nums1.length]; // the length of result won't exceed one of the arrays -> at most, the two arrays are identical
    int index = 0;
    for (int i = 0; i < nums2.length; i++) {
        if (set.contains(nums2[i])) {
            res[index++] = nums2[i];
            set.remove(nums2[i]); // in case of duplicate
        }
    }
    
    return Arrays.copyOfRange(res, 0, index);
    
    /*
    // solution 2: Sort + 2 Pointers
    int[] res = new int[nums1.length];
    Arrays.sort(nums1);
    Arrays.sort(nums2);
    int p1 = 0;
    int p2 = 0;
    int i = 0;
    while (p1 < nums1.length && p2 < nums2.length) {
        if (nums1[p1] == nums2[p2]) {
            if (i == 0 || nums1[p1] != res[i - 1]) {
                res[i++] = nums1[p1];
            }
            p1++;
            p2++;
        } else if (nums1[p1] < nums2[p2]) {
            p1++;
        } else {
            p2++;
        }
    }
        
    return Arrays.copyOfRange(res, 0, i); 
    */   
}
```

### 

### 5. Note:

* My first attempt was to store result in a **HashSet&lt;Integer&gt;**, and finally convert the set to an **int\[\]** with:
  * collection.stream\(\).mapToInt\(x -&gt; x\).toArray\(\);
  * collection.stream\(\).mapToInt\(Number::intValue\).toArray\(\);
  * it consumes a lot of time, so a better solution is to create a long enough array at first, and copy to a smaller one after we got the valid length.
* To copy an array:
  * Arrays.copyOfRange\(AnyType\[\] source, int from, int to\)
  * Arrays.copyOf\(AnyType\[\] source, int newLength\)
  * System.arraycopy\(AnyType\[\] source, int sourceStart, AnyType\[\] target, int targetStart, int length\)

