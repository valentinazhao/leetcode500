[链表重排序](https://leetcode.com/problems/reorder-list/description/)

```
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You must do this in-place without altering the nodes' values.

For example,
Given {1,2,3,4}, reorder it to {1,4,2,3}.
````

```java
public class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null || head.next.next == null) {
            return;
        }
        // split into two halves
        ListNode fast = head.next;
        ListNode slow = head;
        while (fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
        }
        fast = slow.next;
        slow.next = null;
        // reverse the second half
        fast = reverse(fast);
    
        // merge
        merge(head, fast);
    }
    
    public ListNode reverse(ListNode head){       
        if (head.next == null) {
            return head;
        }

        ListNode curr = head;
        ListNode prev = null;
        
        while(curr.next != null){
            ListNode tmp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = tmp;
        }
        curr.next = prev;
        
        return curr;        
    }

    private void merge(ListNode head, ListNode head2) {
        ListNode curr = head;

        while (head2 != null) {
            ListNode tmp = head2;
            head2 = head2.next;
            tmp.next = curr.next;
            curr.next = tmp;    
            curr = tmp.next;
        }
    }
}
