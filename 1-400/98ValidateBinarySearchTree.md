[验证而叉搜索树](https://leetcode.com/problems/validate-binary-search-tree/description/)

```
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
Example 1:
    2
   / \
  1   3
Binary tree [2,1,3], return true.
Example 2:
    1
   / \
  2   3
Binary tree [1,2,3], return false.
```

```java
public class Solution {
    public boolean isValidBST(TreeNode root) {
        Stack<TreeNode> s = new Stack<>();
        TreeNode curr = root;
        TreeNode prev = null;
        
        while(!s.isEmpty() || curr != null) {
            while(curr != null) {
                s.push(curr);
                curr = curr.left;
            }
            curr = s.pop();
            if(prev != null && prev.val >= curr.val) {
                return false;
            }
            prev = curr;
            curr = curr.right;
        }
        
        return true;
    }    
}
```
