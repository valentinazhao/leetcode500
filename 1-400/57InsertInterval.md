[插入区间](https://leetcode.com/problems/insert-interval/description/)

```
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

Example 1:
Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].

Example 2:
Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].

This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

```

```java
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> result = new ArrayList<>();
        int idx = 0;
        
        while (idx < intervals.size() && intervals.get(idx).start < newInterval.start) {
            idx++;
        }
        intervals.add(idx, newInterval);
        
        Interval last = null;
        for (Interval item: intervals) {
            if (last == null || item.start > last.end) {
                result.add(item);
                last = item;
            } else {
                last.end = Math.max(last.end, item.end);
            }
        }
        
        return result;
    }
}
```