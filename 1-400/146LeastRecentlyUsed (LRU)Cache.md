[LRU](https://leetcode.com/problems/lru-cache/description/)

```
Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

Follow up:
Could you do both operations in O(1) time complexity?

Example:

LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

分清楚哪些涉及哪个几个操作->function.
```java
class LRUCache {
    class ListNode {
        int key, value;
        ListNode prev, next;
        public ListNode (int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    
    public int cap, count;
    public ListNode head, tail;
    public HashMap<Integer, ListNode> map;

    public LRUCache(int capacity) {
        this.cap = capacity;
        map = new HashMap<>();
        head = new ListNode(-1, -1);
        tail = new ListNode(-1, -1);
        head.next = tail;
        tail.prev = head;
        tail.next = null;
        head.prev = null;
        count = 0;
    }
    
    public void deleteNode(ListNode target) {
        target.prev.next = target.next;
        target.next.prev = target.prev;
    }
    
    public void addToHead(ListNode target) {
        target.next = head.next;
        head.next.prev = target;
        head.next = target;
        target.prev = head;
    }
    
    public int get(int key) {
        if (map.containsKey(key)) {
            ListNode node = map.get(key);
            deleteNode(node);
            addToHead(node);
            return node.value;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        // we have such node in cache
        if (map.get(key) != null) {
            ListNode old = map.get(key);
            old.value = value;
            deleteNode(old);
            addToHead(old);
        } else {
            ListNode node = new ListNode(key, value);
            map.put(key, node);
            if (count < this.cap) {
                count ++;
            } else {
                map.remove(tail.prev.key);
                deleteNode(tail.prev);
            }
            addToHead(node);
        }
    }
}
````
