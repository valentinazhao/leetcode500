[字符串之字形转换](https://leetcode.com/problems/zigzag-conversion/description/)

```
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

string convert(string text, int nRows);
convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".
```
一道无聊的数学题
```java
public class Solution {
    public String convert(String s, int numRows) {
        char[] c = s.toCharArray();
        int len = c.length;
        StringBuffer[] sb = new StringBuffer[numRows];
        for (int i = 0; i < sb.length; i++) sb[i] = new StringBuffer();
        
        int i = 0;
        while (i < len){
            for (int idx = 0; idx < numRows && i < len; idx++) sb[idx].append(c[i++]);
            for (int idx = numRows - 2; idx >= 1 && i< len; idx--) sb[idx].append(c[i++]);
        }
        
        for (int idx = 1; idx < sb.length; idx++) sb[0].append(sb[idx]);
        return sb[0].toString();
    }
}
```
