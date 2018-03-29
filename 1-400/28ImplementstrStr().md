[KMP](https://leetcode.com/problems/implement-strstr/description/)

```
Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:

Input: haystack = "hello", needle = "ll"
Output: 2
Example 2:

Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle == null || needle.length() == 0) {
            return 0;
        } 
        if (haystack == null || haystack.length() == 0) {
            return -1;
        }
        
        char[] ch = needle.toCharArray();
        int[] next = makeNext(ch);
        
        for (int i = 0, j = 0; i < haystack.length();) {
            if (j == -1 || haystack.charAt(i) == ch[j]) {
                j ++;
                i ++;
                if (j == ch.length) {
                    return i - j;
                }
            }
            if (i < haystack.length() && haystack.charAt(i) != ch[j]) {
                j = next[j];
            }
        }
        
        return -1;
    }
    private int[] makeNext(char[] ch) {
        int n = ch.length;
        int[] next = new int[n];
        
        next[0] = -1;
        for (int i = 0, j = -1; i + 1< n;) {
            if (j == -1 || ch[i] == ch[j]) {
                next[i + 1] = j + 1;
                if (ch[i + 1] == ch[j + 1]) {
                    next[i + 1] = next[j + 1];
                }
                i ++;
                j ++;
            }
            if (ch[i] != ch[j]) {
                j = next[j];
            }
        }
        
        return next;
    }
}
```
