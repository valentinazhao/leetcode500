[搜索一个范围](https://leetcode.com/problems/search-for-a-range/description/)

```
Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example,
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].
```

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums.length == 0 || nums == null) {
            return new int[]{-1, -1};
        }
        int[] res = new int[2];
        
        // left bound;
        int leftBound = binarySearch(target, nums);  
        if (leftBound == nums.length || nums[leftBound] != target) {
            return new int[]{-1, -1};
        } else {
            res[0] = leftBound;
        }
        
        // right bound;
        int rightBound = binarySearch(target + 1, nums); 
        //System.out.println("target = " + target + ", left=" + left);
        res[1] = rightBound - 1;
        
        return res;   
    }
    
    private int binarySearch(int target, int[] nums) {
        int left = 0, right = nums.length, mid;
        while (left < right) {
            mid = left + (right - left) / 2;
            if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left; // left有两种可能
    }
}
```
