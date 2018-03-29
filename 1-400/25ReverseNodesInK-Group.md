
```java
public class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if ( head == null || k <= 1) return head;
    
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        int count = k;
    
        while (head != null){
            count --;
            if (count == 0){
                prev = reverse(prev, head.next);
                head = prev.next;
                count = k;
            } else {
                head = head.next;
            }
        }
        return dummy.next;
    }
    
    public ListNode reverse(ListNode preHead, ListNode nextHead){
        ListNode tail = preHead.next;
        ListNode curr = tail.next;
    
        while(curr != nextHead){
            ListNode tmp = curr.next;
            curr.next = preHead.next;
            preHead.next = curr;
            curr = tmp;
        }
        tail.next = nextHead;   
        return tail;
    }
}
```
