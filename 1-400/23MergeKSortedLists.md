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
public class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        int n = lists.length;
        if (lists == null || n == 0) return null;
        
        while (n > 1){
            int k = (n + 1) / 2;
            for (int i = 0; i < n/2; i++) {
                lists[i] = mergeTwoLists(lists[i], lists[i + k]);
            }
            n = k;
        }
    
        return lists[0];   
    }
    
    public ListNode mergeTwoLists(ListNode l1, ListNode l2){        
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        
        if (l1.val < l2.val){
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }else{
            l2.next = mergeTwoLists(l2.next, l1);
            return l2;
        }       
    }
}
```
