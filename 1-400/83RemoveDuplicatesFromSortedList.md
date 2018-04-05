[从排序链表中移除重复](https://leetcode.com/problems/remove-duplicates-from-sorted-list/description/)

```
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.
```

```java
public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null) {
            return null;
        } 
        
        ListNode prev = head;
        ListNode curr = head.next;
        while(curr != null) {
            if(curr.val != prev.val) {
                prev.next = curr;
                prev = prev.next;
            } 
                curr = curr.next;
                if(curr == null) {
                    prev.next = null;
                }
            
        }
        
        return head;
    }
}
```
