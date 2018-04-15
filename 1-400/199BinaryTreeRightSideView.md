[二叉树右视图](https://leetcode.com/problems/binary-tree-right-side-view/description/)


```
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:
Given the following binary tree,

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
 

You should return [1, 3, 4].
```


```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        getRightView(root, 0, result);
        return result;
    }
    
    public void getRightView(TreeNode root, int currentDepth, List<Integer> result){
        if(root==null)
            return;
        if(currentDepth == result.size()){
            result.add(root.val);
        }
        getRightView(root.right, currentDepth + 1, result);
        getRightView(root.left, currentDepth + 1, result);
    }
}
```


```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
          List<Integer> list = new LinkedList<Integer>();
          Queue<TreeNode> queue = new LinkedList<TreeNode>();

          if(root == null) {
              return list;
          }
          queue.add(root);

          while(!queue.isEmpty()) {
              int m = queue.size();
              while(m > 0) {
                  TreeNode node = queue.remove();
                  if(node.left != null) {
                      queue.add(node.left);
                  }
                  if(node.right != null) {
                      queue.add(node.right);
                  }
                  m--;
                  if(m == 0) {
                      list.add(node.val);
                  }
              }
          }
          
          return list;    
    }
}
```
