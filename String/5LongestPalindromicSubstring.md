[最长回文串](https://leetcode.com/problems/longest-palindromic-substring/description/)

```
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example:

Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.
 

Example:

Input: "cbbd"

Output: "bb"
```

#### Solution 1
中心扩展法
Time complexity O(n*n) 
```java
public class Solution {
	int max = 0, start = 0, end = 0;
	public String longestPalindrome(String s) {
	    	if(s == null || s.length() < 2) {
            return s;
        }
        for(int i = 0; i < s.length(); i++) {
            findPalindrome(s, i, i);
            if(i + 1 < s.length() && s.charAt(i) == s.charAt(i + 1)) {
                findPalindrome(s, i, i + 1);
            }
        }
            
        return s.substring(start, end + 1);
    } 
    
    private void findPalindrome(String str, int l, int r) {
        while(l - 1 >= 0 && r + 1 < str.length() && str.charAt(l - 1) == str.charAt(r + 1)) {
            l--;
            r++;
        }
        if(r - l + 1 > max) {
            max = r - l + 1;
            start = l;
            end = r;
        }
    }
}
```

#### Solution 2
DP </br>
      1. P[i, j] = P[i+1, j-1]， if s[i] = s[j] </br>
      2. P[i, j] = 0，if s[i] != s[j] </br>
```java
public class Solution {    
	public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }
        
        int n = s.length(), start = 0, end = 0, len = 0;
        boolean[][] dp = new boolean[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = i; j >= 0; j--) {
                if (s.charAt(i) == s.charAt(j) && ((i - j) < 3 || dp[j + 1][i - 1])) {
                    dp[j][i] = true;
                    if (i - j > len) {
                        len = i - j;
                        start = j;
                        end = i;
                    }
                }
            }
        }
        
        return s.substring(start, end + 1);
    } 
}
```
