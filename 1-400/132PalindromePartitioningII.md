[拆分回文串之二](https://leetcode.com/problems/palindrome-partitioning-ii/description/)

```
Given a string s, partition s such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of s.

For example, given s = "aab",
Return 1 since the palindrome partitioning ["aa","b"] could be produced using 1 cut.
```
这题cache的方法还是会TLE, 只能用DP </br>
在哪里切 + 在某处切之前最小几刀   //    [i][j]表示某段是否回文, 此处最小值如何表示 </br>
So we need two cache arraysone tracks the partition position and one tracks the number of minimum cut.
https://www.programcreek.com/2014/04/leetcode-palindrome-partitioning-ii-java/

```java
class Solution {
    public int minCut(String s) {
        int n = s.length();
        
        boolean[][] dp = new boolean[n][n];
        int[] cut =  new int[n];
        
        for (int i = 0; i < n; i++) {
            cut[i] = i;
            for (int j = 0; j <= i; j++) {
                if (s.charAt(j) == s.charAt(i) && (i - j <= 1 || dp[j + 1][i - 1])) {
                    dp[j][i] = true;
                    if (j == 0) {
                        cut[i] = 0;
                    } else {
                        cut[i] = Math.min(cut[i], cut[j - 1] + 1);
                    }
                }
            }
        }
        
        return cut[n - 1];
    }
}
```
注： 网上包括discussion解法杂乱，多找找不同blog，找自己能理解的非常重要.
