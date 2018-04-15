[二进制数字中1的个数](https://leetcode.com/problems/number-of-1-bits/description/)


```
Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.
```



移位操作
```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            if ((n & 1) == 1) {
                count++;
            }
            n = n >>> 1;
        }
        return count;
        
    }
}
```

使用n&(n-1)的方法, 发现有几个1，就循环几次n&(n-1)得到0
```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int cnt = 0;
        while (n != 0) {
            n = n & (n - 1);
            cnt ++;
        }
        
        return cnt;
    }
}
```
