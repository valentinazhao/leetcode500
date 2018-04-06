[二叉树层序遍历](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)

```
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
```

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        helper(root, 0, res);
        return res;
    }
    public void helper(TreeNode root, int level, List<List<Integer>> res) {
        if(root == null) return ;
        if(level == res.size()) res.add(new LinkedList<>());
        res.get(level).add(root.val);
        helper(root.left, level + 1, res);
        helper(root.right, level + 1, res);
    }
}
```
