[二叉树之字形层序遍历](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/)

```
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its zigzag level order traversal as:
[
  [3],
  [20,9],
  [15,7]
]
```

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        helper(root, 0, res);
        return res;
    }
    public void helper(TreeNode root, int level, List<List<Integer>> res) {
        if(root == null) return ;
        if(level == res.size()) {
            res.add(new LinkedList<>());
        }
        if(level % 2 == 0) {
            res.get(level).add(root.val);
        } else {
            res.get(level).add(0, root.val);
        }
        helper(root.left, level + 1, res);
        helper(root.right, level + 1, res);
    }
}
```
