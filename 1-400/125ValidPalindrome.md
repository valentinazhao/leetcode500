[验证回文字符串](https://leetcode.com/problems/valid-palindrome/description/)

```
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

Note:
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.
```

```java
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0,  right = s.length() - 1;
        
        while (left <= right) {
            char ch1 = s.charAt(left), ch2 = s.charAt(right);
            if (!Character.isLetterOrDigit(ch1)) {
                left ++;
            } else if (!Character.isLetterOrDigit(ch2)) {
                right --;
            } else {
                if (Character.toLowerCase(ch1) != Character.toLowerCase(ch2)) {
                    return false;
                }
                left ++;
                right --;
            }
        }
        
        return true;
    }
}
```
