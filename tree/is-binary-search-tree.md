---
description: BST
---

# Is Binary Search Tree

### 1. Description

Determine if a given binary tree is binary search tree.There should no be duplicate keys in binary search tree.

**Assumptions**

* You can assume the keys stored in the binary search tree can not be Integer.MIN\_VALUE or Integer.MAX\_VALUE.

**Corner Cases**

* What if the binary tree is null? Return true in this case.



### 2. Solution

* BST feature: `node.left.value < node.value < node.right.value`
* DFS: pass the range of node value for determination
  * base case: 
    * node == null: return true;
    * node.value exceeds the boundaries: return false;
  * recursive rule:
    * check left child
    * check right child
    * return the AND result

{% hint style="info" %}
Complexity:

* Time: O\(n\) 

where n represents the total amount of nodes in tree

because the determination\(boundary check\) for each node takes O\(1\) and there are n nodes in total

* Space: O\(height\)
{% endhint %}



### 3. JAVA Implementation

```text
 public class TreeNode {
    public int key;
    public TreeNode left;
    public TreeNode right;
    public TreeNode(int key) {
      this.key = key;
    }
 }
 
public boolean isBST(TreeNode root) {
    if (root == null) {
        return true;
    }
    
    return checkBounds(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
}

private boolean checkBounds(TreeNode root, int min, int max) {
    if (root == null) {
        return true;
    }
    
    if (root.key <= min || root.key >= max) {
        return false;
    }
    
    return checkBounds(root.left, min, root.key) && checkBounds(root.right, root.key, max);
}
```



### 4. Comments

* Assumption: no duplicates in BST

