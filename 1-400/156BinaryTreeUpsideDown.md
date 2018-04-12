[二叉树的上下颠倒](https://leetcode.com/problems/binary-tree-upside-down/description/)


```
Given a binary tree where all the right nodes are either leaf nodes with a sibling (a left node that shares the same parent node) or empty, flip it upside down and turn it into a tree where the original right nodes turned into left leaf nodes. Return the new root.

For example:
Given a binary tree {1,2,3,4,5},

    1
   / \
  2   3
 / \
4   5
 
return the root of the binary tree [4,5,2,#,#,3,1].

   4
  / \
 5   2
    / \
   3   1  
   
OJ's Binary Tree Serialization:

The serialization of a binary tree follows a 【level order traversal】, where '#' signifies a path terminator where no node exists below.

Here's an example:

   1
  / \
 2   3
    /
   4
    \
     5
The above binary tree is serialized as "{1,2,3,#,#,4,#,#,5}"
```

初级水平
```java
class Solution {
    private boolean flag = true;
    private TreeNode rst = null;
    public TreeNode upsideDownBinaryTree(TreeNode root) {
        if(root == null || root.left == null && root.right == null) return root;
        helper(root);
        return rst;
    }
    
    public TreeNode helper(TreeNode root) {
        if(root == null || (root.left == null && root.right == null || root.left == null)) {
            return root;
        }
        TreeNode left = helper(root.left);
        TreeNode right = helper(root.right);
        
        left.left = right;
        left.right = root;
        root.left = null;
        root.right = null;
        
        if(flag) {
            rst = left;
            flag = false;
        }
        
        return root;
    }
}
```

高级水平
```java
class Solution {
    public TreeNode upsideDownBinaryTree(TreeNode root) {
	TreeNode node = root, parent = null, left = null, right = null;
	
	while (node != null) {
            left = node.left;
            node.left = right;
	    right = node.right;
            node.right = parent;
	    parent = node;
	    node = left;
	}
        
	return parent;
    } 
}
````
