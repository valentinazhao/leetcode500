[二叉树最短深度](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)

```
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
```

```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        
        Stack<TreeNode> st = new Stack<>();
        Stack<Integer> sv = new Stack<>();
        st.push(root);
        sv.push(1);
        int min = Integer.MAX_VALUE;
    
        while (!st.isEmpty()) {
            TreeNode curr = st.pop();
            int temp = sv.pop();
            if (curr.left == null && curr.right == null) {
                min = Math.min(temp, min);
            }
            
            if (curr.left != null) {
                st.push(curr.left);
                sv.push(temp + 1);
            }
            if (curr.right != null) {
                st.push(curr.right);
                sv.push(temp + 1);
            }       
        }
        
        return min == Integer.MAX_VALUE? 1 : min;
    }
}
```
