[二叉搜索树迭代器](https://leetcode.com/problems/binary-search-tree-iterator/description/)


```
Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling next() will return the next smallest number in the BST.

Note: next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.
```

这道题主要就是考二叉树的中序遍历的非递归形式(啊啊啊啊...
```java
public class BSTIterator {
    public Stack<TreeNode> stack = new Stack<>();
    
    public BSTIterator(TreeNode root) {
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        if (stack.isEmpty()) {
            return false;
        }
        return true;
    }

    /** @return the next smallest number */
    public int next() {
        TreeNode node = stack.pop();
        int rst = node.val;
        if (node.right != null) {
            node = node.right;
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
        }
        return rst;
    }
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = new BSTIterator(root);
 * while (i.hasNext()) v[f()] = i.next();
 */
 ```
