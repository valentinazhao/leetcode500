[找旋转排序数组中的最小值](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/description/)


```
Follow up for "Find Minimum in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

The array may contain duplicates(有重复).
```

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


错误代码
Input: [3,1]  Wrong Answer: 3
```java
class Solution {
    public int findMin(int[] nums) {
        int start = 0, end = nums.length - 1;
        
        while (start < end) {
            int mid = start + (end - start) / 2;
            // 6701245 5670124 4567012
            if (nums[mid] < nums[end]) {
                end = mid;
            } else if (nums[mid] > nums[start]) {  start = mid + 1 说明排除了mid这个端点 你这样写是排除了start这个端点...
                start = mid + 1;
            } else {
                end --;
            }
        }
        
        return nums[start];
    }
}
```
