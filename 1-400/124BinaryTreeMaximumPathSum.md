[二叉树的最大路径和](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/)

```
Given a binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

For example:
Given the below binary tree,

       1
      / \
     2   3
Return 6.
```

```java
class Solution {
    private int max = Integer.MIN_VALUE;
    
    public int maxPathSum(TreeNode root) {
        int maxSub = helper(root); 
        return max;
    }
    
    public int helper(TreeNode root) {
        if(root == null) return 0;
        if(root.left == null && root.right == null) {
            max = Math.max(max, root.val);
            return root.val;
        }
        int left = Math.max(0, helper(root.left));
        int right = Math.max(0, helper(root.right));
        max = Math.max(max, left + right + root.val);
        return Math.max(left, right) + root.val;
    }   
}
````
