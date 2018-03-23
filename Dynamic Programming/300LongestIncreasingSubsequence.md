[最长递增子序列](https://leetcode.com/problems/longest-increasing-subsequence/description/)

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        if (nums == null || n == 0) {
            return 0;
        }
        
        int result = 0;
        int[] dp = new int[n];
        Arrays.fill(dp, 1);
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[j] + 1, dp[i]);
                }
            }
            result = Math.max(result, dp[i]);
        }
        
        return result;
    }
}
```
