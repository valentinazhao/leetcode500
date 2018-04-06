[倒置链表之二](https://leetcode.com/problems/reverse-linked-list-ii/description/)

```
Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

Note:
Given m, n satisfy the following condition:
1 ≤ m ≤ n ≤ length of list.
```

```java
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode curr =  new ListNode(0);
        curr.next = head;
        ListNode fast = curr;
        // fast points to node(1)
        for(int i = 0; i < m - 1; i++) {
            System.out.println("!!!!");
            fast = fast.next;
        }
        // second stores original head of interval(in this case, it's 2)
        ListNode first = fast, second = fast.next;
        curr = second;
        ListNode prev = null;
        for(int i = 0; i < n - m + 1; i++) {
            System.out.println("????");
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        
        first.next = prev;
        second.next = curr;
        
        // return first.next 与 head 区别: 关键是head所指这个node有没有被改动过！就这一点！一般肯定return head. But，如果m == 1，随着
        // first改动，head所指node会被移动到最后，此时first所指才是头结点.
        return m != 1 ? head : first.next;
    }
}
```
