[求x的n次方](https://leetcode.com/problems/powx-n/description/)

```
Implement pow(x, n).
```

```java
class Solution {
    public double myPow(double x, int n) {
        if (n < 0) {
            return 1 / power(x, -n);
        } else if (n == 0) {
            return 1;
        } else {
            return power(x, n);
        }
    }
    private double power (double x, int n) {
        if (n == 0) return 1.0;
        double res = power(x, n / 2);
        if (n % 2 == 0) {
            return res * res;
        }
        
        return res * res * x;
    }
}
```
