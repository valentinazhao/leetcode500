[求根到叶子节点之和](https://leetcode.com/problems/sum-root-to-leaf-numbers/description/)

```
Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

For example,

    1
   / \
  2   3
 

The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.

Return the sum = 12 + 13 = 25.
```

```java
class Solution {
    public int sumNumbers(TreeNode root) {
        return helper(root, 0);
    }
    
    private int helper(TreeNode root, int pathSum) {
        if (root == null) return 0;
        if (root.left == null && root.right == null) return pathSum * 10 + root.val;
        
        return helper(root.left, pathSum * 10 + root.val) + helper(root.right, pathSum * 10 + root.val);
    }
}
```
