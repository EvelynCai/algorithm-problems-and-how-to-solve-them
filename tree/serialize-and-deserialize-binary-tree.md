---
description: Tree
---

# 297. Serialize and Deserialize Binary Tree

### 1. [Description](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)

  
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Example:** 

```text
You may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as "[1,2,3,null,null,4,5]"
```

**Clarification:** The above format is the same as [how LeetCode serializes a binary tree](https://leetcode.com/faq/#binary-tree). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.



### 2. Solution

To serialize the tree into a string, my intuition is to traverse it in some order. 

So to determine traverse in what order, we have to think about how can we deserialize the string back to a tree:

Generally speaking, if I want to build a tree, there are 2 key features I need to figure out:

* tree structure \(i.e. at what position it's a real node, at what position it's a null\)
* node value, i.e. if a node exists at an exact position, what's it value

Since we are asked to build a tree from one string, there is one more thing we should consider:

* how can we get all the valid values from the string, i.e. the "invalid" separator among valid tree node values

Therefore, I first think about level-order traversal. 

**2.1 Pre-order Traversal \(DFS\)**

Since preOrder means we visit tree nodes in the order recursively: root -&gt; leftChild -&gt; rightChild, in the recursion of deserialization, the first value we see is always a "root" for current sub-tree, except NULL.

Therefore, there are 2 points to note:

* handler of NULL TreeNode: use special char to record in serialization + recover NULL and immediately return \(i.e. hit the current bottom\) in deserialization
* we need First-In-First-Out data structure to record the order to deserialize, so Queue is our choice

**2.2 Level-order Traversal \(BFS\)**

TBC

{% hint style="info" %}
* Time: O\(n\)  

where n represents the amount of nodes in tree because we need to traverse all nodes and visiting each node takes O\(1\).  N.B.  In serialization, remember to use StringBuilder instead of String so that we make sure each node takes O\(1\) time to update the final result. 

* Space: O\(n\)  

where n represents the amount of nodes in tree. Because in deserialization, the recursion stack would take extra space for all the node if tree is extremely skewed. Also, the Queue of values takes O\(n\) time because each node maps a value.
{% endhint %}



### 3. JAVA Implementation

3.1 DFS \(preOrder Traversal\)

```text
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) {
            return null;
        }
        
        StringBuilder sb = new StringBuilder();
        seHelper(root, sb);
        sb.deleteCharAt(sb.length() - 1); // delete the last  sep, ","
        System.out.println(sb.toString());
        return sb.toString();
    }
    
    private void seHelper(TreeNode root, StringBuilder sb) {
        if (root == null) {
            sb.append("#").append(","); // use "#" to represent null TreeNode
            return;
        }
        
        sb.append(root.val).append(",");
        
        seHelper(root.left, sb);
        seHelper(root.right, sb);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data == null) {
            return null;
        }
        
        Queue<String> q = new LinkedList<>(); // use String instead of Integer, because there could be "#"
        String[] vals = data.split(",");
        for (String s: vals) {
            q.offer(s);
        }
        
        return deHelper(q);
    }
    
    private TreeNode deHelper(Queue<String> q) {
        if (q.isEmpty()) {
            return null;
        }
        
        String top = q.poll();
        if (top.equals("#")) { // not work if use top == "#"
            return null;
        }
        
        int nodeVal = Integer.parseInt(top);
        TreeNode root = new TreeNode(nodeVal);
        root.left = deHelper(q);
        root.right = deHelper(q);
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```



### 4. Notes

* To compare Strings, use string1.equals\(string2\) instead of  "string1 == string2". Because ".equals\(\)" is comparing values and "==" is comparing references.



### 5. Extension

* [145. Binary Tree Postorder Traversal](https://app.gitbook.com/@alittlebit/s/data-structures-and-algorithms-in-java/145.-binary-tree-postorder-traversal)
* [449. Serialize and Deserialize BST](https://app.gitbook.com/@alittlebit/s/algorithm-problems-and-how-to-solve-them/tree/449.-serialize-and-deserialize-bst)
* 428. Serialize and Deserialize N-ary Tree

