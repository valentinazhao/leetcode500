[找旋转有序数组的最小值](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

```
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

You may assume no duplicate(无重复元素) exists in the array.
```


搜索问题,马上联想到二分法
```java
class Solution {
    public int findMin(int[] nums) {
        int start = 0, end = nums.length - 1;
        
        while (start < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] > nums[end]) {
                start = mid + 1;
            } else {
                end = mid;
            }
        }
        
        return nums[start];
    }
}
```

错误代码
Input: [2,1] Wrong Answer: 2
```java
class Solution {
    public int findMin(int[] nums) {
        int start = 0, end = nums.length - 1;      
        while (start < end) {
            int mid = start + (end - start) / 2;
            if (nums[start] < nums[mid]) {  // 都nums[start] < nums[mid] 肯定错过最小值啦..
                start = mid + 1;
            } else {
                end = mid;
            }
        }      
        return nums[start];
    }
}
```
