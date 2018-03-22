[爬楼梯](https://leetcode.com/problems/climbing-stairs/description/)

```java
class Solution {
    public int climbStairs(int n) {
        // initialize
        int[] f = new int[n + 1];
        f[0] = 1;
        f[1] = 1;
        
        // function
        for (int i = 2; i <= n; i++) {
            f[i] = f[i - 1] + f[i - 2];
        }
        
        // answer
        return f[n];
    }
}
```
