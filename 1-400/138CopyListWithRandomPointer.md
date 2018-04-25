[拷贝带有随机指针的链表](https://leetcode.com/problems/copy-list-with-random-pointer/description/)

```
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.
```


这题重新仔细一看发现自己写的逻辑有问题..
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



```java
Time: Access eache node TWICE - O(2n)
Space: HashMap - O(n)
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return head;
        }
        
        // mapping: old -> new
        Map<RandomListNode, RandomListNode> map = new HashMap<>();
        
        RandomListNode cur = head; // start with old head;
        while (cur != null) {
            // 1. create nodes of current, next, random
            if (!map.containsKey(cur)) {
                RandomListNode newNode = new RandomListNode(cur.label);
                map.put(cur, newNode);
            }
            if (cur.next != null && !map.containsKey(cur.next)) {
                RandomListNode nextNode = new RandomListNode(cur.next.label);
                map.put(cur.next, nextNode);
            }
            if (cur.random != null && !map.containsKey(cur.random)) {
                RandomListNode randNode = new RandomListNode(cur.random.label);
                map.put(cur.random, randNode);
            }
            // 2. connect current with next, random
            if (cur.next != null) {
                map.get(cur).next = map.get(cur.next);
            }
            if (cur.random != null) {
                map.get(cur).random = map.get(cur.random);
            }
            // 3. next round
            cur = cur.next;
        }
        
        return map.get(head);
    }
}
```



```java
Improvement: Can we do it without HashMap?
How to store the mapping?  Next!
Assumption: Can we change input?
分三步:
1th_Pass: Copy Next
2nd_Pass: Copy Random
3rd_Pass: Split_LL
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return head;
        }
        
        RandomListNode cur = head;
        while (cur != null) {
            RandomListNode temp = cur.next;
            RandomListNode node = new RandomListNode(cur.label);
            cur.next = node;
            node.next = temp;
            cur = cur.next.next;
        }
        
        cur = head;
        while (cur != null) {
            if (cur.random != null) {
                cur.next.random = cur.random.next;
            }
            cur = cur.next.next;
        }
        
        cur = head;
        RandomListNode dummy = new RandomListNode(0);
        dummy.next = cur.next;
        while (cur != null) {
            RandomListNode node = cur.next.next;
            if (node != null) cur.next.next = node.next;
            cur.next = node; //这题
            cur = node;
        }
        
        return dummy.next;
    }
}
```

