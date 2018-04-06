[唯一二叉搜索树之二](https://leetcode.com/problems/unique-binary-search-trees-ii/description/)

```
Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example,
Given n = 3, your program should return all 5 unique BST's shown below.

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

```java
public class Solution {
    public List<TreeNode> generateTrees(int n) {
    List<TreeNode> res = new ArrayList<>();
    if(n == 0) {
        return res;
    }
    res = helper(1, n);
    return res;
}
public List<TreeNode> helper(int start, int end) {
    List<TreeNode> res = new ArrayList<>();
    if(start > end) {
        res.add(null);
        return res;
    }
    for(int k = start; k <= end; k++) {
        List<TreeNode> leftSub = helper(start, k - 1);
        List<TreeNode> rightSub = helper(k + 1, end);
        for (TreeNode i : leftSub) {
            for (TreeNode j : rightSub) {
            TreeNode root = new TreeNode(k);
                root.left = i;
                root.right = j;
                res.add(root);
            }
        }
    }
    
    return res;
    }
}
```
