[求阶乘末尾零的个数](https://leetcode.com/problems/factorial-trailing-zeroes/description/)


```
Given an integer n, return the number of trailing zeroes in n!.

Note: Your solution should be in logarithmic time complexity.
```

```
让求一个数的阶乘末尾0的个数，也就是要找乘数中10的个数，而10可分解为2和5，而我们可知2的数量又远大于5的数量，那么此题即便为找出5的个数。
仍需注意的一点就是，像25,125，这样的不只含有一个5的数字需要考虑进去。

```

```java
class Solution {
    public int trailingZeroes(int n) {
        int rst = 0;
        
        while (n > 0) {
            rst += n / 5;
            n /= 5;
        }
        
        return rst;
    }
}
```


```java
class Solution {
    public int trailingZeroes(int n) {
        return n > 0 ? trailingZeroes(n / 5) + n / 5 : 0;
    }
}
```
