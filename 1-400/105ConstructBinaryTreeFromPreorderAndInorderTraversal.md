[由前序遍历和中序遍历建立二叉树](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)

```
Given preorder and inorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given

preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
Return the following binary tree:

    3
   / \
  9  20
    /  \
   15   7
```

```java
public class Solution {   
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder == null|| inorder == null|| preorder.length != inorder.length) return null;
        TreeNode head = rebuildHelper(preorder, 0, inorder, 0, inorder.length - 1);
        return head;
    }
    
    public TreeNode rebuildHelper(int[] pre, int prestart, int[] in, int instart, int inend) {
        if(instart > inend || prestart > pre.length - 1) return null;
        //else if( prestart == preend) return new TreeNode(pre[prestart]);
        int data = pre[prestart];
        int index = findIndex(in, instart, inend, data);
        if(index == -1) return null;
        TreeNode root = new TreeNode(data);
        int len = index - instart;
        root.left = rebuildHelper(pre, prestart + 1, in, instart, index - 1);
        root.right = rebuildHelper(pre, prestart + 1 + len, in, index + 1, inend);
        return root;
    }
    
    public int findIndex(int[] nums, int start, int end, int target) {
        for (int t = start; t < end + 1; t ++) {
            if (nums[t] == target) {
                return t;
            }
        }
        return -1;
    }   
}
```
