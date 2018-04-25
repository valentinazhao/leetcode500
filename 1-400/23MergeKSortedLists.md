[合并K个有序链表](https://leetcode.com/problems/merge-k-sorted-lists/description/)

Solution 1: PQ
```java
public class Solution {
    public ListNode mergeKLists(List<ListNode> lists) {
        if (lists==null||lists.size()==0) return null;
        
        PriorityQueue<ListNode> queue= new PriorityQueue<ListNode>(lists.size(),new Comparator<ListNode>(){
            @Override
            public int compare(ListNode o1,ListNode o2){
                if (o1.val<o2.val)
                    return -1;
                else if (o1.val==o2.val)
                    return 0;
                else 
                    return 1;
            }
        });
        
        ListNode dummy = new ListNode(0);
        ListNode tail=dummy;
        
        for (ListNode node:lists)
            if (node!=null)
                queue.add(node);
            
        while (!queue.isEmpty()){
            tail.next=queue.poll();
            tail=tail.next;
            
            if (tail.next!=null)
                queue.add(tail.next);
        }
        return dummy.next;
    }
}
```

Solution 2
```java
/**have a priorityqueue pq, put all the first node in the lists to the pq
 * poll the node with smallest val from pq, add the node to the tail, and add the node.next to the pq
 * ListNode is not comparable, so we need to creat a comparator and pass to the pq
 * space complexity O(len) len is length of the lists
 * time complexity O(nlog(len)) n is total number of nodes, and log(len) is cost for update the pq each time when adding a new node
 */
class Solution {
    private class NodeOrder implements Comparator<ListNode> {
        @Override
        public int compare(ListNode l1, ListNode l2) {
            return l1.val - l2.val;
        }
    }
    public Comparator<ListNode> valOrder() {
        return new NodeOrder();
    }
    
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;
        int n = lists.length;
        PriorityQueue<ListNode> pq = new PriorityQueue<ListNode>(n, valOrder());
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        
        for (ListNode node : lists) {
            if (node != null) pq.add(node);
        }
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            if(node.next != null) pq.add(node.next);
            tail.next = node;
            tail = tail.next;
        }
        return dummy.next;
    }
}

/** idea based on two list merge, divide the lists into two parts, merge them seperately, and then do two lists merge
 *  similar to mergeSort
 *  time complexity (O(nlog(len)) n is the total number of nodes, len is the length of the lists.
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;
        return mergeLists(lists, 0, lists.length - 1);
    }
    private ListNode mergeLists(ListNode[] lists, int lo, int hi) {
        if (lo > hi) return null;
        if (lo == hi) return lists[lo];
        int mid = (hi-lo)/2 + lo;
        ListNode left = mergeLists(lists, lo, mid);
        ListNode right = mergeLists(lists, mid + 1, hi);
        return mergeTwoLists(left, right);
    }
    private ListNode mergeTwoLists(ListNode left, ListNode right) {
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        while(left != null && right != null) {
            if (left.val <= right.val) {
                tail.next = left;
                left = left.next;
            }
            else {
                tail.next = right;
                right = right.next;
            }
            tail = tail.next;
        }
        if (left == null) tail.next = right;
        if (right == null) tail.next = left;
        return dummy.next;
    }
}
```
