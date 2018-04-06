[由中序和后序遍历构建二叉树](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)

```
Given inorder and postorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given

inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]
Return the following binary tree:

    3
   / \
  9  20
    /  \
   15   7
```

```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if(postorder == null|| inorder == null|| postorder.length != inorder.length) return null;
        TreeNode head = rebuildHelper(postorder, postorder.length - 1, inorder, 0, inorder.length - 1);
        return head;
    }
    public TreeNode rebuildHelper(int[] post, int postend, int[] in, int instart, int inend) {
        if(instart > inend || 0 > postend) return null;
        //else if( poststart == postend) return new TreeNode(post[poststart]);
        int data = post[postend];
        int index = findIndex(in, instart, inend, data);
        if(index == -1) return null;
        TreeNode root = new TreeNode(data);
        int len = inend - index;
        root.left = rebuildHelper(post, postend - len - 1, in, instart, index - 1);
        root.right = rebuildHelper(post, postend - 1, in, index + 1, inend);
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
