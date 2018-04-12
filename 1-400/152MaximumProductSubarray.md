[子数组最大乘积](https://leetcode.com/problems/maximum-product-subarray/description/)

```
Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.
```

注意到对数组中每一步来说，如果正数，make result bigger, other wise负数, smaller. 只有两种结果. 所以每走一步，比较更新结果即可.
```java
class Solution {
    public int maxProduct(int[] a) {
        if (a == null || a.length == 0) {
            return Integer.MIN_VALUE;
        }
        
        int n = a.length, rst = a[0], min = a[0], max = a[0];
        for (int i = 1; i < n; i++) {
            if (a[i] < 0) {
                int temp = max;
                max = min;
                min = temp;
            }
            min = Math.min(a[i], a[i] * min);  // 注意, 不是 min = Math.min(min, a[i] * min)
            max = Math.max(a[i], a[i] * max);  // 题目要求两相邻数字，不是全局最大值. 如[2,3,-2,4] 6不是8
            
            rst = Math.max(max, rst);
        }
        
        return rst;
    }
}
````
