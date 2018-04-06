[恢复二叉搜索树](https://leetcode.com/problems/recover-binary-search-tree/description/)

```
Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

Note:
A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?
```

```java
class Solution {   
    public void recoverTree(TreeNode root) {
        if(root == null) {
        return;
    }
    Stack<TreeNode> s = new Stack<>();
    TreeNode first = null;
    TreeNode second = null;
    
    TreeNode prev = null;
    TreeNode curr = root;
    while(!s.isEmpty() || curr != null) {
        while(curr != null) {
            s.push(curr);
            curr = curr.left;
        }
        curr = s.pop();
        if(prev != null && prev.val >= curr.val) {
            if(first == null) {
                first = prev;
            }
            second = curr;
        }
        prev = curr;
        curr = curr.right;
    }
        
    int tmp = first.val;
    first.val = second.val;
    second.val = tmp;
    }
}
```
