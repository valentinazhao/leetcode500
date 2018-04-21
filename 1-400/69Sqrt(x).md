[平方根](https://leetcode.com/problems/sqrtx/description/)

```
Implement int sqrt(int x).

Compute and return the square root of x.

x is guaranteed to be a non-negative integer.


Example 1:

Input: 4
Output: 2
Example 2:

Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we want to return an integer, the decimal part will be truncated.
```

```
这题很神秘啊.. left竟然从0开始，要知道start inclusive的...

```
```java
public class Solution {
    public int mySqrt(int x) {
        if(x <= 1) return x;
        int start = 0, end = x;
        while(start <= end) {
            int mid = start + (end - start) / 2;
            if(x / mid == mid) 
                return mid;
            else if(x / mid < mid)
                end = mid - 1;
            else
                start = mid + 1;
        }
        
        return end;
    }
}
```
或者
```java
public class Solution {
    public int mySqrt(int x) {
        if (x <= 1) {
            return x;
        }
        int left = 0, right = x;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (x / mid == mid) {
                return mid;
            } else if (x / mid < mid) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        //System.out.println(left + ", " + right);
        if (x / left >= left) return left;
        return left - 1;
    }
}
```
