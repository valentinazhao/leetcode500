[求末尾单词的长度](https://leetcode.com/problems/length-of-last-word/description/)

```
Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

Example:

Input: "Hello World"
Output: 5
```

```java
class Solution {
    public int lengthOfLastWord(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        
        char[] ch = s.toCharArray();
        int result = 0, count = 0;
        for (int i = 0; i < ch.length; i++) {
            if (ch[i] == ' ') {
                count = 0;
            } else {
                count ++;
                result = count;
            }
        }
        
        return result;
    }
}
```
