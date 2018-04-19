[帕斯卡三角形之二](https://leetcode.com/problems/pascals-triangle-ii/description/)

```
Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return [1,3,3,1].

Note:
Could you optimize your algorithm to use only O(k) extra space?
```

```java
倒着来的原因画图即可知（为了不覆盖要重复利用的数）
public class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> result = new ArrayList<>();
        result.add(1);
        if (rowIndex == 0) {
            return result;
        }
        
        for (int i = 1; i <= rowIndex; i++) {
            result.add(1);
            int size = result.size();
            for (int j = size - 2; j >= 1; j--) {
                result.set(j, result.get(j) + result.get(j - 1));
            }
        }
        
        return result;
    }
}
```
