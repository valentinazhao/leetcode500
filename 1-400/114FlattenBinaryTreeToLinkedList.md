[将二叉树展成链表](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)

```
Given a binary tree, flatten it to a linked list in-place.

For example,
Given

         1
        / \
       2   5
      / \   \
     3   4   6
The flattened tree should look like:
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
```
注意题目何为"in-place"？ 不然的话可以用中序遍历tree，另起炉灶build linkedlist
```java
public class Solution {
    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }
        if (root.left != null) {
            flatten(root.left);
        }
        if (root.right != null) {
            flatten(root.right);
        }
        TreeNode lastNode = root.right;
        root.right = root.left;
        root.left = null;
        while (root.right != null) {
            root = root.right;
        }
        root.right = lastNode;
    }
}
```
