[Excel表格列转换](https://leetcode.com/problems/excel-sheet-column-number/description/)



```
Related to question Excel Sheet Column Title

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```



```java
class Solution {
    public int titleToNumber(String s) {
        int base = 'A' - 1;
        
        int rst = 0;
        char[] ch = s.toCharArray();
        for (int i = 0; i < ch.length; i++) {
            rst = rst * 26 + ch[i] - base;
        }
        
        return rst;
    }
}
```
