[移除链表倒数第N个数](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

```
Given a linked list, remove the nth node from the end of list and return its head.

For example,

   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:
Given n will always be valid.
Try to do this in one pass.
```

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        // Null pointer Exception
        
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode nthNode = head;
        
        // 向后移动n步
        while (nthNode != null && n > 0) {
            nthNode = nthNode.next;
            n --;
        }
        
        if (nthNode == null) {
            dummy.next = head.next;
        } else {
            while (nthNode.next != null) {
                head = head.next;
                nthNode = nthNode.next;
            }
            head.next = head.next.next;
        }
        
        return dummy.next;
    }
}
```
