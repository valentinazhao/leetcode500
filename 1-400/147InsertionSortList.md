[链表插入排序](https://leetcode.com/problems/insertion-sort-list/description/)

```
Sort a linked list using insertion sort.
```

```java
class Solution {
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        
        while (head != null) {
            ListNode curr = dummy;
            while (curr.next != null && curr.next.val <= head.val) {
                curr = curr.next;
            }
            ListNode temp = head.next;
            head.next = curr.next;
            curr.next = head;
            head = temp;
        }
        
        return dummy.next;
    }
}
````
