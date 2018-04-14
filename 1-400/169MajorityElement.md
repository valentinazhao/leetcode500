[求众数](https://leetcode.com/problems/majority-element/description/)


```
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.
```

Boyer-Moore Majority Vote Algorithm - Time O(n) Space O(1)
```java
class Solution {
    public int majorityElement(int[] nums) {
        int res = 0, cnt = 0;
        for (int num: nums) {
            if (cnt == 0) {
                res = num;
                cnt ++;
            } else if (num == res) {
                cnt ++;
            } else {
                cnt --;
            }
        }
        
        return res;
    }
}
```

Binary Search
```java
class Solution {
    public int majorityElement(int[] nums) {
        return major(nums, 0, nums.length - 1);
    }
    
    private int major(int[] nums, int left, int right) {
        if (left == right) return nums[left];
        int mid = left + (right - left) / 2;
        int lm = major(nums, left, mid);
        int rm = major(nums, mid + 1, right);
        if (lm == rm) return rm;
        return getCount(nums, left, mid, lm) > getCount(nums, mid + 1, right, rm) ? lm : rm;
    }
    
    private int getCount(int[] nums, int left, int right, int val) {
        int cnt = 0;
        for (int i = left; i <= right; i++) {
            if (nums[i] == val) cnt++;    
        }    
        return cnt;
    }
}
```

