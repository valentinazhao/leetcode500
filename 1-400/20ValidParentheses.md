[验证括号](https://leetcode.com/problems/valid-parentheses/description/)

```java
class Solution {
    public boolean isValid(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }
        
        Stack<Character> stack = new Stack<>();
        char[] ch = s.toCharArray();
        for (int i = 0; i < ch.length; i++) {
            char c = ch[i];
            if (c == ')' || c == '}' || c == ']') {
                if (stack.isEmpty() || stack.pop() != c) {
                    return false;
                }
            } else {
                if (c == '(') {
                    stack.push(')');
                } else if (c == '{') {
                    stack.push('}');
                } else {
                    stack.push(']');
                }
            }
        }
        if (!stack.isEmpty()) {
            return false;
        }
        
        return true;
    }
}
```
