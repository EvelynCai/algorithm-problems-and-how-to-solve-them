---
description: HashTable
---

# Top k Frequent Words

### 1. [Description](https://leetcode.com/problems/top-k-frequent-words/)

Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

**Example 1:**

```text
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
    Note that "i" comes before "love" due to a lower alphabetical order.
```

**Example 2:**

```text
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
    with the number of occurrence being 4, 3, 2 and 1 respectively.
```

**Note:**

1. You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
2. Input words contain only lowercase letters.

**Follow up:**

1. Try to solve it in O\(n log k\) time and O\(n\) extra space.

### 2. Solution

HashTable + Heap

1. Use HashTable to count the word frequencies
2. Use Heap to get the Top k Frequent Element
   1. customize the comparator of heap based on HashTable
   2. reuse any one of the solutions of Top k Frequent Element

{% hint style="info" %}
Complexity:

* Time: O\(nlogn\)

where n represent the length of input array

because iterate input array to count freq - O\(n\)

                heapify k elements in minHeap - O\(k\)

                update \(n - k\) elements in minHeap if necessary - O\(\(n - k\) logk\)

in total = O\(n + \(n - k\) logk\)

* Space: O\(n\)

because the hash table takes a max of O\(n\) extra space and the heap takes O\(k\)
{% endhint %}

### 3. JAVA Implementation

```text
public List<String> topKFrequent(String[] words, int k) {
        Map<String, Integer> map = new HashMap<>();
        PriorityQueue<String> pq = new PriorityQueue<>((w1, w2) -> {
            if (map.get(w1) == map.get(w2)) {
                return w2.compareTo(w1);
            } else {
                return map.get(w1) - map.get(w2);
            }
        });
        
        for (String s: words) {
            map.put(s, map.getOrDefault(s, 0) + 1);
        }
        
        for (String key: map.keySet()) {
            pq.offer(key);
            if (pq.size() > k) {
                pq.poll();
            }
        }
        
        List<String> res = new ArrayList<>();
        while (!pq.isEmpty()) {
            res.add(pq.poll());
        }
        Collections.reverse(res);
        return res;
}
```

```text
Map<String, Integer> dict = new HashMap<>();

private class dictComparator implements Comparator<String> {
    @Override
      public int compare(String a, String b) {
        int freqA = dict.get(a);
        int freqB = dict.get(b);
        return freqA - freqB;
      }
}

public String[] topKFrequent(String[] combo, int k) {
    if (combo == null || combo.length == 0) {
      return combo;
    }
    
    for (String s: combo) {
      int freq = dict.getOrDefault(s, 0);
      dict.put(s, freq + 1);
    }

    // corner case: k > #distinctWords
    if (dict.keySet().size() <= k) {
      k = dict.keySet().size();
    }
    
    PriorityQueue<String> pq = new PriorityQueue<>(k, new dictComparator());
    for (String key: dict.keySet()) {
      if (pq.size() < k) { // NO <=
        pq.offer(key);
      } else {
        int freqTop = dict.get(pq.peek());
        int freqTemp = dict.get(key);
        if (freqTop < freqTemp) {
          pq.poll();
          pq.offer(key);
        }
      }
    }

    String[] result = new String[k];
    for(int i = k - 1; i >= 0; i--) {
      result[i] = pq.poll();
    }
    return result;
}
```

### 4. Comments

* A key assumption: k ? \#distinctWord
  * do we always have k &lt;= \#distinctWord?



