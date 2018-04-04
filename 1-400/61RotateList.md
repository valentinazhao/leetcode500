[旋转链表](https://leetcode.com/problems/rotate-list/description/)

```
Given a list, rotate the list to the right by k places, where k is non-negative.


Example:

Given 1->2->3->4->5->NULL and k = 2,

return 4->5->1->2->3->NULL.
```

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null || head.next == null){
            return head;
        }
        
        int length = this.getListLength(head);
        k = k % length;
        if(k == 0){
            return head;
        }
        
        ListNode p = head;
        ListNode preNode = null;
        for(int i = 0; i < length - k; i++){
            preNode = p;
            p = p.next;
        }
        preNode.next = null;
        ListNode newHead = p;
        while(p != null){
            preNode = p;
            p = p.next;
        }
        preNode.next = head;
        
        return newHead;        
    }
    public int getListLength(ListNode head){
        ListNode p = head;
        int length = 0;
        while(p != null){
            p = p.next;
            length++;
        }
        return length;
    }
}
```
