[二叉树层序遍历之二](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/description/)

```
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
]
```

```java
public class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) {
            return res;
        }
        
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while(!q.isEmpty()) {
            List<Integer> tmpList = new ArrayList<>();
            int size = q.size();
            for(int i = 0; i < size; i ++) {
                TreeNode tmp = q.poll();
                tmpList.add(tmp.val);
                if(tmp.left != null) {
                    q.offer(tmp.left);
                }
                if(tmp.right != null) {
                    q.offer(tmp.right);
                }
            }
            res.add(tmpList);
        }
        Collections.reverse(res);
        return res;
    }
}
```
