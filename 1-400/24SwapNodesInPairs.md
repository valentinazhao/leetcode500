[成对交换结点](https://leetcode.com/problems/swap-nodes-in-pairs/description/)

```java
public class Solution {
    public ListNode swapPairs(ListNode head) {
    
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode curr = dummy;
    
    while (curr != null && curr.next != null && curr.next.next != null){
        ListNode nNode = curr.next;
        ListNode nnNode = curr.next.next;
        curr.next = nnNode;
        nNode.next = nnNode.next;
        nnNode.next = nNode;
        curr = curr.next.next;    
    }
    
    return dummy.next;
    }
}
```
