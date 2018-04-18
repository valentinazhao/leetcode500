[平衡二叉树](https://leetcode.com/problems/balanced-binary-tree/description/)

```
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example 1:

Given the following tree [3,9,20,null,null,15,7]:

    3
   / \
  9  20
    /  \
   15   7
Return true.

Example 2:

Given the following tree [1,2,2,3,3,null,null,4,4]:

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
Return false.
```

Solution 1: without resultType
```java
class Solution {
    public boolean isBalanced(TreeNode root){
        if (root == null) {
            return true;
        }
        int left = getDepth(root.left);
        if (left == -1) {
            return false;
        }
        int right = getDepth(root.right);
        if (right == -1) {
            return false;
        }
        
        return (left - right) < 2 && (left - right) > -2;
    }

    public int getDepth(TreeNode node) {
        if (node == null) {
            return 0;
        }
        int left = getDepth(node.left);
        if (left == -1) {
            return -1;
        }
        int right = getDepth(node.right);
        if (right == -1) {
            return -1;
        }
        if ((left - right) >= 2 || (right - left) >= 2) return -1;
        
        return Math.max(left, right) + 1;
    }
}
```

Solution 2: Return Type
```java
class Solution {
    class Cell {
        int height;
        boolean flag;
        public Cell(int h, boolean flag) {
            this.height = h;
            this.flag = flag;
        }       
    }
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        Cell result = helper(root);
        return result.flag;
    }
    private Cell helper(TreeNode root) {
        if (root == null) {
            return new Cell(0, true);
        }
        
        Cell left = helper(root.left);
        Cell right = helper(root.right);
        
        Cell result = new Cell(Math.max(left.height, right.height) + 1, true);
        
        if (Math.abs(left.height - right.height) > 1 || !left.flag || !right.flag) {
            result.flag = false;       
        }
        
        return result;
    }
}
```
