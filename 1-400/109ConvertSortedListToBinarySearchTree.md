[将有序链表转换成二叉搜索树](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/description/)

```
Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.


Example:

Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

```java
public class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        return helper(head, null);    
    }
    
    public TreeNode helper(ListNode start, ListNode end) {
        if (start == end) {
            return null;    
        }
        ListNode fast = start;
        ListNode slow = start;
        while(fast != end && fast.next != end) {
            slow = slow.next;
            fast = fast.next.next;
        }
        TreeNode node = new TreeNode(slow.val);
        node.left = helper(start, slow);
        node.right = helper(slow.next, end);
        return node;
    }    
}
```
