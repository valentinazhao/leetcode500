[二叉树最长连续序列](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/description/)


```
Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

For example,
   1
    \
     3
    / \
   2   4
        \
         5
Longest consecutive sequence path is 3-4-5, so return 3.
   2
    \
     3
    / 
   2    
  / 
 1
Longest consecutive sequence path is 2-3,not3-2-1, so return 2.
```

Top down - Avoid global variable
```java
class Solution {
    public int longestConsecutive(TreeNode root) {
        return helper(root, Integer.MAX_VALUE, 0);
    }
    private int helper(TreeNode root, int pre, int len) {
        if (root == null) {
            return len;
        }
        if ((pre + 1) == root.val) {
            len ++;
        } else {
            len = 1;
        }
        
        int left = helper(root.left, root.val, len);
        int right = helper(root.right, root.val, len);
        
        return Math.max(Math.max(left, right), len); 
    } 
}
```


bottom up - Avoid global variable
```java
有难度
```
