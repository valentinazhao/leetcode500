[验证回文数字](https://leetcode.com/problems/palindrome-number/description/)

```java
public class Solution {
    public boolean isPalindrome(int x) { 
        if(x < 0) {
            return false;
        }
        String s = Integer.toString(x);
        int i = 0, count = s.length() / 2;
        while(count > 0) {
            if(s.charAt(i) != s.charAt(s.length() - i - 1)) {
                return false;
            }
            i++;
            count--;
        }
        
        return true;
    }
}
```
