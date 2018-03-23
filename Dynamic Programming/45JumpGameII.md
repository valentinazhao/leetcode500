[跳跃游戏之二](https://leetcode.com/problems/jump-game-ii/description/)

DP
```java
public class Solution {
    public int jump(int[] A) {
        int n = A.length;
        int[] dp = new int[n];
        for (int i = 0; i < n; i++) {
            dp[i] = 0;
            for (int j = 0; j < i; j++) {
                if (j + A[j] >= i) {
                    dp[i] = dp[j]+1;
                    break;
                }
            }
        }
        return dp[n-1];
    }
}
```
