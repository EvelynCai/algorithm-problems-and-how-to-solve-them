---
description: DFS
---

# All Permutations of Subsets

### 1. Description

Given a string with no duplicate characters, return a list with all permutations of the string and all its subsets.

Examples

Set = “abc”, all permutations are \[“”, “a”, “ab”, “abc”, “ac”, “acb”, “b”, “ba”, “bac”, “bc”, “bca”, “c”, “cb”, “cba”, “ca”, “cab”\].

Set = “”, all permutations are \[“”\].

Set = null, all permutations are \[\].  


### 2. Solution

DFS \(combine subset \* permutation\)

{% hint style="info" %}
Complexity

* Time: O\(2 ^ N \* m!\)

where n represents the length of input string

subset O\(2 ^ n\) -  generates 2 ^ n subsets to permute

permutation O\(m!\) - where m represents the length of subset string, \[0, n\]

* Space: O\(n\)
{% endhint %}

### 3. JAVA Implementation

```text
public List<String> allPermutationsOfSubsets(String set) {
    List<String> res = new ArrayList<>();
    if (set == null) {
      return res;
    }
  
    getSubsets(set, 0, new StringBuilder(), res);
    List<String> subsets = new ArrayList<>(res);
    
    Map<String, Boolean> map = new HashMap<>();
    for (String s: subsets) {
      String key = getKey(s);
      if (!map.containsKey(key)) {
        map.put(key, true);
        permute(s.toCharArray(), 0, res, s);
      }
    }

    return res;
  }

private String getKey(String s) {
    char[] arr = s.toCharArray();
    Arrays.sort(arr);
    return new String(arr);
}

private void getSubsets(String s, int level, StringBuilder sb, List<String> res) {
    if (level >= s.length()) {
      res.add(sb.toString());
      return;
    }

    sb.append(s.charAt(level));
    getSubsets(s, level + 1, sb, res);

    sb.deleteCharAt(sb.length() - 1);
    getSubsets(s, level + 1, sb, res);
}

private void permute(char[] chars, int level, List<String> res, String s) {
    if (level >= chars.length) {
      String tmp = String.valueOf(chars);
      if (!tmp.equals(s)) {
        res.add(String.valueOf(chars));
      }
      return;
    }

    for (int i = level; i < chars.length; i++) {
      swap(chars, i, level);
      permute(chars, level + 1, res, s);
      swap(chars, i, level);
    }
}

private void swap(char[] chars, int a, int b) {
    char tmp = chars[a];
    chars[a] = chars[b];
    chars[b] = tmp;
}
```

### 4. Comments

* Deduplicate:
  * use HashSet to store permutation results
  * use HashMap&lt;String, Boolean&gt; to store if the key \(sorted lexicographically\) has been permuted or not 

