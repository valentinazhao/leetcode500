[最长有效括号长度](https://leetcode.com/problems/longest-valid-parentheses/description/)

Solution 1: DP
```java
class Solution {
    public int longestValidParentheses(String s) {
        int n = s.length();
        if (s == null || n == 0) {
            return 0;
        }
        
        char[] ch = s.toCharArray();
        int[] dp = new int[ch.length];
        int result = 0;
        
        for (int i = 1; i < ch.length; i++) {
            if (ch[i] == ')') {
                if (ch[i - 1] == '(') {
                    dp[i] = i - 2 >= 0 ? dp[i - 2] + 2 : 2;
                } else {
                    if (i - dp[i - 1] - 1 >= 0 && ch[i - dp[i - 1] - 1] == '(') {
                        dp[i] = dp[i - 1] + 2 + (i - dp[i - 1] - 2 >= 0 ? dp[i - dp[i - 1] - 2] : 0);
                    }
                }
                result = Math.max(result, dp[i]);
            }
        }
        
        return result;
    }
}
```
concise version:
```java
class Solution {
    public int longestValidParentheses(String s) {
        int n = s.length();
        if (s == null || n == 0) {
            return 0;
        }
        
        char[] ch = s.toCharArray();
        int[] dp = new int[ch.length];
        int result = 0;
        
        for (int i = 1; i < ch.length; i++) {
            if (ch[i] == ')' && i - dp[i - 1] - 1 >= 0 && ch[i - dp[i - 1] - 1] == '(') {
                dp[i] = dp[i - 1] + 2 + (i - dp[i - 1] - 2 >= 0 ? dp[i - dp[i - 1] - 2] : 0);
                result = Math.max(result, dp[i]);
            }
        }
        
        return result;
    }
}
```

Solution 2: Stack
```java

```
