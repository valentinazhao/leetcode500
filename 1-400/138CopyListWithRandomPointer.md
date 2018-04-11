[拷贝带有随机指针的链表](https://leetcode.com/problems/copy-list-with-random-pointer/description/)

```
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.
```

```java
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return head;
        }
        
        RandomListNode root = new RandomListNode(head.label);
        RandomListNode p = root;
        while (head != null) {
            if (head.next != null) {
                p.next = new RandomListNode(head.next.label);
            }
            if (head.random != null) {
                p.random = new RandomListNode(head.random.label);
            }
            p = p.next;
            head = head.next;
        }
        
        return root;
    }
}
````
