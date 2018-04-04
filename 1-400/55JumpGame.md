[跳跃游戏](https://leetcode.com/problems/jump-game/description/)

```
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.
```

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
