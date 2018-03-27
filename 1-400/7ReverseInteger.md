[翻转整数](https://leetcode.com/problems/reverse-integer/description/)

```java
public class Solution {
    public int reverse(int x) {
        int rst = 0;
        while (x != 0) {
            // handle overflow/underflow
            if (Math.abs(rst) > (Integer.MAX_VALUE / 10)) {
                return 0;
            } 
            rst = rst * 10 + x % 10;
            x /= 10;
        }
        return rst;
    }
}
```
