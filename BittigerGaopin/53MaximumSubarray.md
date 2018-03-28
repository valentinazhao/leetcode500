[子数组最大值](https://leetcode.com/problems/maximum-subarray/description/)

```java
class Solution {
    public int maxSubArray(int[] nums) {
        // corner case
        if(nums == null || nums.length == 0) {
            return 0;
        }
        
        int result = nums[0], currSum = 0;
        for (int i = 0; i < nums.length; i++) {
            currSum = currSum > 0 ? currSum + nums[i] : nums[i];
            result = Math.max(result, currSum);
        }
        
        return result;
    }
}
```
