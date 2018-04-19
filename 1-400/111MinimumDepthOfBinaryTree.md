[二叉树最短深度](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)

```
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
```

我日！这什么方法啊。。。
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

自己写的，参考了graph的思想，速度99.67%
```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        int level = 1;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size > 0) {
                TreeNode node = q.poll();
                if (node.left == null && node.right == null) {
                    return level;
                }
                if (node.left != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
                size --;
            }
            level ++;
        }
        
        return 0;
    }
}
```
