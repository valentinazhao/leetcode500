[混合插入有序链表](https://leetcode.com/problems/merge-two-sorted-lists/description/)

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0);
        ListNode dummy = head;
        
        while (l1 != null || l2 != null) {
            ListNode newNode = new ListNode(0);
            if (l1 != null && l2 != null) {
                if (l1.val < l2.val) {
                    newNode.val = l1.val;
                    l1 = l1.next;
                } else {
                    newNode.val = l2.val;
                    l2 = l2.next;
                }
            } else if (l1 != null) {
                newNode.val = l1.val;
                l1 = l1.next;
            } else if (l2 != null) {
                newNode.val = l2.val;
                l2 = l2.next;
            }
            head.next = newNode;
            head = head.next;
        }
        
        return dummy.next;
    }
}
```
