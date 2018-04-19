[路径总和之二](https://leetcode.com/problems/path-sum-ii/description/)

```
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:
Given the below binary tree and sum = 22,
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
return
[
   [5,4,11,2],
   [5,8,4,5]
]
```

```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> tmpList = new ArrayList<>();
        if(root == null) {
            return res;
        }
        helper(root, sum, tmpList, res);
        return res;
    }
    public void helper(TreeNode root, int sum, List<Integer> tmpList, List<List<Integer>> res) {
        tmpList.add(root.val);
        if(root.left == null && root.right == null) {
            if(sum == root.val) {
                res.add(new ArrayList(tmpList)); // 此处写return 的话有个bug，说明此写法有问题
            }
        }
        
        if(root.left != null) {
            helper(root.left, sum - root.val, tmpList, res);
        }
        if(root.right != null) {
            helper(root.right, sum - root.val, tmpList, res);
        }
        
        tmpList.remove(tmpList.size() - 1);
    }
}
```
