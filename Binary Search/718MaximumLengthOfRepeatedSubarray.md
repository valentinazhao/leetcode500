[最长公共子数组](https://leetcode.com/problems/maximum-length-of-repeated-subarray/description/)


```
Given two integer arrays A and B, return the maximum length of an subarray that appears in both arrays.

Example 1:
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
Note:
1 <= len(A), len(B) <= 1000
0 <= A[i], B[i] < 100
```

```
why binary search tag??

And, remember this useful matrix:

    // recurrence formula
    // suffixLength = 1+f(i-1, j-1): a[i]==b[j]
    // suffixLength = 0: a[i]!=n[j]
    // subarrayLengh = max{suffixLength(i, j)}
    
    //   x 1 2 3 2 1
    // x 0 0 0 0 0 0
    // 3 0 0 0 1 0 0
    // 2 0 0 1 0 2 0
    // 1 0
    // 4 0
    // 7 0
    
```

```java
class Solution {
    public int findLength(int[] A, int[] B) {
        if (A == null || B == null || A.length == 0 || B.length == 0) {
            return 0;
        }
        
        int m = A.length, n = B.length, rst = 0;
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (A[i] == B[j]) {
                    dp[i + 1][j + 1] = dp[i][j] + 1;
                    rst = Math.max(rst, dp[i + 1][j + 1]);
                }
            }
        }
        
        return rst;
    }
}
```


```java
        // 1D array, going from backwards to utilize data from i-1
        int[] dp = new int[n+1];
        for(int i = 0; i < m; i++) {
            for(int j = n-1; j >= 0; j--) {
                dp[j+1] = A[i] == B[j] ? dp[j] + 1: 0;
                max = Math.max(dp[j+1], max);
            }
        }
```
