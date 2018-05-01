[将有序数组转换成二叉搜索树](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/)




```
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.


Example:

Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

```
Discussion里有个贴，非常有意思和价值：
What if it's the sorted linkedlist, can we construct the BST from that in O(n)?
https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/discuss/35255/What-if-it's-the-sorted-linkedlist-can-we-construct-the-BST-from-that-in-O(n)


以下是O(n)的方法，但其实也有O(nlogn)的方法，用bs每次找到要insert的target值.


我还有一个疑问，是不是因为这里要BST，因此“int mid = start + (end - start) / 2；”一切为二，如果是三/四...叉树是不是就要想办法分成相应的段数，构建tree.

```

```java
public class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null) {
            return null;
        }
        if (nums.length == 1) {
            TreeNode node = new TreeNode(nums[0]);
            return node;
        }
        return helper(nums, 0, nums.length);
    }
    
    public TreeNode helper(int[] nums, int start, int end) {
        if (start >= end) {
            return null;
        }
        int mid = start + (end - start) / 2; 
        TreeNode node= new TreeNode(nums[mid]);
        node.left = helper(nums, start, mid);
        node.right = helper(nums, mid + 1, end);
        return node;
    }  
}
```
