[计数和发言](https://leetcode.com/problems/count-and-say/description/)

Solution 1: iterative
```java
public class Solution {
    public String countAndSay(int n) { 
        String oldString = "1";
        n -= 1;
        
        while(n > 0) {
            StringBuilder sb = new StringBuilder();
            char[] oldChars = oldString.toCharArray();
            for(int i = 0; i < oldChars.length; i++) {
                int count = 1;
                while((i + 1) < oldChars.length && oldChars[i] == oldChars[i + 1]) {
                    count++;
                    i++;
                }
                sb.append(String.valueOf(count) + String.valueOf(oldChars[i]));
            }
            oldString = sb.toString();
            n--;
        }
        
        return oldString;
    }
}
```

Solution 2: recursive
```java
class Solution {
    public String countAndSay(int n) {
        String result = "1";
        while(n > 1) {
            result = buildString(result);
            n--;
        }
        return result;
    }
    
    public String buildString(String s) {
        if (s.length() == 0) {
            return "";
        }
        
        char[] digits = s.toCharArray();
        StringBuilder builder = new StringBuilder();
        char pre = digits[0];
        int count = 0;
        for(char c : digits) {
            if(c == pre) {
                count++;
            } else {
                builder.append(count);
                builder.append(pre);
                pre = c;
                count = 1;
            }
        }
        builder.append(count);
        builder.append(pre);

        return builder.toString();
    }
}
```
