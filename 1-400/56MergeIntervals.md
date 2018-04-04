[合并区间](https://leetcode.com/problems/merge-intervals/description/)

```
Given a collection of intervals, merge all overlapping intervals.

For example,
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].
```

```java
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> result = new ArrayList<>();
        
        intervals.sort(Comparator.comparing(i -> i.start));
        /*Collection.sort(intervals, new Comparator<Interval>() {
            @Override
            public int compare(Interval a, Interval b) {
                return a.start - b.start;
            }
        }); */
        
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
