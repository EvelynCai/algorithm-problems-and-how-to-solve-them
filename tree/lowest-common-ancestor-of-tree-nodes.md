# Lowest Common Ancestor of Tree Nodes

### Common Sense

1. Lowest Common Ancestor\(LCA\): 

The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants \(where we allow a node to be a descendant of itself\).

2. Tree Node: 

```text
public class TreeNode {
     int val;
     TreeNode left;
     TreeNode right;
     TreeNode(int x) { val = x; }
}
```

### 

### Classical Problems

#### 1.[ Lowest Common Ancestor of a Binary Tree \(236\)](https://app.gitbook.com/@alittlebit/s/data-structures-and-algorithms-in-java/236.-lowest-common-ancestor-of-a-binary-tree)

Given a binary tree, find the  \(LCA\) of two given nodes in the tree.

Given the following binary tree:  root = \[3,5,1,6,2,0,8,null,null,7,4\]

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

Example 1:

```text
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

Example 2:

```text
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

Note / Key Assumptions:

* All of the nodes' values will be unique.
* p and q are different and both values will exist in the binary tree.

=&gt; Analysis: Recursion

* base case: if current node is null / current node is node-to-find -&gt; current node itself is LCA
* recursive rule: ask from left subtree and right subtree
  * if one returns from left subtree, the other from right subtree -&gt; current node is LCA
  * if both return from one subtree -&gt; what's returned is LCA
* complexity:
  * time: \(depends on tree balance\) 
    * worst = O\(n\), 
    * avg = O\(logn\), where n is amount of tree nodes.
  * space: worst = O\(n\) \(extra space taken by recursion stack\)

=&gt; JAVA Implementation:

```text
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root.val == p.val || root.val == q.val) {
            return root;
        }
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left != null && right != null) {
            return root;
        }
        
        return left == null ? right : left;
}
```

#### 2. [Lowest Common Ancestor of a Binary Search Tree \(235\)](https://app.gitbook.com/@alittlebit/s/data-structures-and-algorithms-in-java/235.-lowest-common-ancestor-of-a-binary-search-tree)

Given binary search tree:  root = \[6,2,8,0,4,7,9,null,null,3,5\]

![](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

Example 1:

```text
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA defi
```

Example 2:

```text
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```

Note / Key Assumptions:

* All of the nodes' values will be unique.
* p and q are different and both values will exist in the BST.

=&gt; Analysis: Recursion

* base case: if current node is null -&gt; curr node itself is the LCA
* recursive rule: compare curr.val vs nodeToFind1.val vs nodeToFind2.val
  * curr.val between \[nodeToFind1.val, nodeToFind2.val\] -&gt; curr node itself is the LCA
  * curr.val &lt; both node vals -&gt; recurse to find in right subtree
  * curr.val &gt; both node vals -&gt; recurse to find in left subtree
* complexity:
  * time: \(depends on tree balance\) 
    * worst = O\(n\), 
    * avg = O\(logn\), where n is amount of tree nodes.
  * space: worst = O\(n\) \(extra space taken by recursion stack\)

=&gt; JAVA Implementation:

```text
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return root;
        }
        
        if (root.val < p.val && root.val < q.val) {
            return lowestCommonAncestor(root.right, p, q);
        }
        
        if (root.val > p.val && root.val > q.val) {
            return lowestCommonAncestor(root.left, p, q);
        }
        
        return root;
}
```

#### 3. Lowest Common Ancestor of K Nodes in a N-nary Tree

Assumption: 

* val of each node is unique
* k nodes are all contained in the tree

-&gt; JAVA Implementation:

```text
public class TreeNode {
     int val;
     Set<TreeNode> children;
     TreeNode(int x) { val = x; }
}

public TreeNode lowestCommonAncestor(TreeNode root, Set<TreeNode> nodes) {
        if (root == null || nodes.contains(root)) {
            return root;
        }
           
        int count = 0;        
        TreeNode found = null;
        for (TreeNode child: root.children) {
            TreeNode tmp = lowestCommonAncestor(child, nodes);
            if (tmp != null) {
                found = tmp;
                count++;
            }
        }
        
        return count == nodes.size() ? root : found;
}
```

#### 4. Lowest Common Ancestor of a Binary Tree when Tree Node Contains Parent

-&gt; JAVA Implementation:

```text
public class TreeNode {
     int val;
     TreeNode left;
     TreeNode right;
     TreeNode parent;
     TreeNode(int x) { val = x; }
}

public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return root;
        }
        
        int pDepth = getDepth(p);
        int qDepth = getDepth(q);
        int dist = pDepth - qDepth;
        
        if (dist < 0) {
            TreeNode tmp = p;
            p = q;
            q = tmp;
            dist = -dist;
        }
        
        // now the node p is sure to be deeper, move it up by 'dist' levels
        while (dist != 0) {
            p = p.parent;
        }
        
        // now the nodes, p and q, are at the same level
        while (p != null && q != null) {
            if (p == q) {
                return p;
            }
            
            p = p.parent;
            q = q.parent;
        }
        
        return null;
}

private int getDepth(TreeNode node) {
    int depth = 0;
    while (node != null) {
        depth++;
        node = node.parent;
    }
    
    return depth;
}
```

#### 5. Lowest Common Ancestor of Potentially-non-exist Nodes in Binary Tree

Assumption:

* Target nodes may not exist in the binary tree

Solution:

* if neither node is found, no LCA in the tree
* if both nodes are found, the returned node\(neither target1 nor target2\) is LCA
* if only one node is found
  * both exist, but one is the child of the other
  * only one exists, the other is not in the binary tree 
  * -&gt; check if the found node contains the not-found node:
    * if found, LCA is the parent node
    * if not, no LCA because one node is not in the tree 

-&gt; JAVA Implementation:

```text
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root.val == p.val || root.val == q.val) {
        return root;
    }
    
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    if (left != null && right != null) {
        return root;
    }
    if (left == null && right == null) {
        return null;
    }
    
    TreeNode found = (left == null) ? right : left;
    TreeNode notFound = (left == null) ? left : right;
    if (containCheck(found, notFound)) {
        return found;
    }
    return null;
}

private boolean containCheck(TreeNode found, TreeNode notFound) {
    if (found == null) {
        return false;
    }
    
    if (found == notFound) {
        return true;
    }
    
    return containCheck(found.left, notFound) || containCheck(found.right, notFound);
}
```



#### [6. Lowest Common Manager](https://app.gitbook.com/@alittlebit/s/data-structures-and-algorithms-in-java/common-manager)

Ref:

* With parent pointer: [https://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-tree-set-2-using-parent-pointer/](https://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-tree-set-2-using-parent-pointer/)
* Assume non-exist target nodes: [https://gist.github.com/Lcjc/538709c0c1e15d70efb14d5d93220462](https://gist.github.com/Lcjc/538709c0c1e15d70efb14d5d93220462)

