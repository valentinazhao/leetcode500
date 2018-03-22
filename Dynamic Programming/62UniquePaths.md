[路径搜寻](https://leetcode.com/problems/unique-paths/description/)

```java
class Solution {
    public int uniquePaths(int m, int n) {
        if (m == 0 && n == 0) {
            return 0;
        }else if (m == 0 || n == 0) {
            return 1;
        }
        
        int[][] sum = new int[m][n];
        // initialize
        for (int i = 0; i < m; i++) {
            sum[i][0] = 1;
        }
        for (int i = 0; i < n; i++) {
            sum[0][i] = 1;
        }
        
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                // function
                sum[i][j] = sum[i - 1][j] + sum[i][j - 1];
            }
        }
        
        // answer
        return sum[m - 1][n - 1];
    }
}
```
