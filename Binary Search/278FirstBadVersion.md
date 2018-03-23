[第一个错误的代码版本](https://leetcode.com/problems/first-bad-version/description/)

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int start = 1, end = n;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (isBadVersion(mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
            
        if (isBadVersion(start)) {
            return start;
        }
        return end;
    }
}
```
