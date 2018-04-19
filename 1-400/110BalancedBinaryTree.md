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

Solution 1: Top-down 
```java
The first method checks whether the tree is balanced strictly according to the definition of balanced binary tree: the difference between the heights of the two sub trees are not bigger than 1, and both the left sub tree and right sub tree are also balanced. With the helper function depth(), we could easily write the code;

class Solution {
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        int left = getDepth(root.left);
        int right = getDepth(root.right);
        return Math.abs(left - right) <= 1 && isBalanced(root.left) && isBalanced(root.right);
    }
    private int getDepth(TreeNode node) {
        if (node == null) {
            return -1;
        }
        return Math.max(getDepth(node.left), getDepth(node.right)) + 1;
    }
}
For the current node root, calling depth() for its left and right children actually has to access all of its children, thus the complexity is O(N). We do this for each node in the tree, so the overall complexity of isBalanced will be O(N^2). 
```



Solution 2: Return Type - Bottom-up Time Complexity O(n)
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
