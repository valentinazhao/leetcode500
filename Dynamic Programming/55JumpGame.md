[跳跃游戏之一](https://leetcode.com/problems/jump-game/description/)

```java
class Solution {
    public boolean canJump(int[] nums) {
        if (nums == null || nums.length == 0) {
            return true;
        }
        
        int n = nums.length;
        int[] sum = new int[n];
        for (int i = 1; i < n; i++) {
            sum[i] = Math.max(sum[i - 1], nums[i - 1]) - 1;
            if (sum[i] < 0) {
                return false;
            }         
        }
        
        return sum[n - 1] >= 0;
    }
}
```
