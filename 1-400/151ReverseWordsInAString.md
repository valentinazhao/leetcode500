[翻转字符串中的单词](https://leetcode.com/problems/reverse-words-in-a-string/description/)


```
Given an input string, reverse the string word by word.

For example,
Given s = "the sky is blue",
return "blue is sky the".

Update (2015-02-12):
For C programmers: Try to solve it in-place in O(1) space.

click to show clarification.

Clarification:
What constitutes a word?
A sequence of non-space characters constitutes a word.
Could the input string contain leading or trailing spaces?
Yes. However, your reversed string should not contain leading or trailing spaces.
How about multiple spaces between two words?
Reduce them to a single space in the reversed string.
```


```java
public class Solution {
    public String reverseWords(String s) {
        if (s.length() < 1) return s;
        
        char[] ch = s.toCharArray();
        reverse(ch, 0, ch.length - 1);
        
        int storedIndex = 0;
        for (int i = 0; i < ch.length; i++) {
            if (ch[i] != ' ') {
                if (storedIndex != 0) ch[storedIndex++] = ' ';
                int j = i;
                while (j < ch.length && ch[j] != ' ') {
                    ch[storedIndex++] = ch[j++];
                }
                reverse(ch, storedIndex - (j - i), storedIndex - 1);
                i = j;
            }
        }
        
        return new String(ch, 0, storedIndex);
    }
    
    private void reverse(char[] ch, int start, int end) {
        for (; start < end; start ++, end --) {
            char tmp = ch[end];
            ch[end] = ch[start];
            ch[start] = tmp;
        }
    }
}
```
