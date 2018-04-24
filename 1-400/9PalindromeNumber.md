[验证回文数字](https://leetcode.com/problems/palindrome-number/description/)

```
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:

Input: 121
Output: true
Example 2:

Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
Follow up:

Coud you solve it without converting the integer to a string?
```


```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        
        // convert to char[]
        char[] ch = ("" + x).toCharArray();
        int i = 0, j = ch.length - 1;
        while (i < j) {
            if (ch[i] != ch[j]) {
                return false;
            } else {
                i ++;
                j --;
            }
        }
        
        return true;
    }
}
```

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        
        int num = 0, temp = x;
        while (temp > 0) {
            num = num * 10 + temp % 10;
            temp /= 10;
        }
        
        return num == x;
    }
}
```
