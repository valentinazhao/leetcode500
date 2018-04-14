[缺失区间](https://leetcode.com/problems/missing-ranges/description/)


```
Given a sorted integer array where the range of elements are in the inclusive range [lower, upper], return its missing ranges.

For example, given [0, 1, 3, 50, 75], lower = 0 and upper = 99, return ["2", "4->49", "51->74", "76->99"].
```


```java
class Solution {
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> result = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            addRange(result, lower, upper);
            return result;
        }
        if (lower < nums[0]) {
            addRange(result, lower, (long)nums[0] - 1);
        }
        for (int i = 1; i < nums.length; i++) {
            addRange(result, (long)nums[i - 1] + 1, (long)nums[i] - 1);
        }
        if (nums[nums.length - 1] < upper) {
            addRange(result, (long)nums[nums.length - 1] + 1, (long)(upper));
        }
        return result;
        
    }
    public void addRange(List<String> result, long start, long end) {
        if (start > end) {
            return;
        }
        if (start == end) {
            result.add(start + "");
        } else {
            result.add(start + "->" + end);
        }
    }
}
```
