[二叉树前序遍历](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)

```
Given a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree [1,null,2,3],
   1
    \
     2
    /
   3
return [1,2,3].

Note: Recursive solution is trivial, could you do it iteratively?
````


````java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        
        Stack<TreeNode> s = new Stack<>();
        TreeNode curr = root;
        while (curr != null || !s.isEmpty()) {
            while (curr != null) {
                s.push(curr);
                res.add(curr.val);
                curr = curr.left;
            }
            curr = s.pop();
            curr = curr.right;
        }
        
        return res;
    }
}
```
