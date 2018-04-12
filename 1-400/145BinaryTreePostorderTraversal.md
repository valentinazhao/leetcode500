[二叉树后序遍历](https://leetcode.com/problems/binary-tree-postorder-traversal/description/)

```
Given a binary tree, return the postorder traversal of its nodes' values.

For example:
Given binary tree [1,null,2,3],

   1
    \
     2
    /
   3
 

return [3,2,1].

Note: Recursive solution is trivial, could you do it iteratively?
````

````java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        
        Stack<TreeNode> s = new Stack<>();
        TreeNode curr = root， prev = null;
        
        while (curr != null || !s.isEmpty()) {
            while (curr.left != null) {
                s.push(curr);
                prev = curr;
                curr = curr.left;
            }
            result.add(curr.val);
            if (prev.right != null) {
                s.push(prev.right);
            }
        }
        
        return result;
    }
}
````
