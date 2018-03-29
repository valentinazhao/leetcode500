[有序数组中去除重复元素](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int index = 0, i = 0;
        while (i < nums.length) {
            int number = nums[i];
            while (i < nums.length && nums[i] == number) {
                i++;
            }
            nums[index++] = number;
        }
        
        return index;
    }
}
```
