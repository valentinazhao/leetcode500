[寻找旋转有序数组的最小值之二](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/description/)

```java
class Solution {
    public int findMin(int[] nums) {
        int start = 0, end = nums.length - 1;
        
        while (start < end) {
            int mid = start + (end - start) / 2;
            // 6701245 5670124 4567012
            if (nums[mid] < nums[end]) {
                end = mid;
            } else if (nums[mid] > nums[end]) {
                start = mid + 1;
            } else {
                end --;
            }
        }
        
        return nums[start];
    }
}
```
