[进制转换](https://leetcode.com/problems/excel-sheet-column-title/description/)


```
Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```


```java
class Solution {
    public String convertToTitle(int n) {       
        StringBuilder res = new StringBuilder();
        while (n > 0){
            res.append((n % 26) != 0 ? (char)((n % 26) + 'A'- 1) : (char)('Z'));
            n = (n - 1) / 26;
        }
       
        return res.reverse().toString();
    }
}
