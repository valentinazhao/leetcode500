[帕斯卡三角形之二](https://leetcode.com/problems/pascals-triangle-ii/description/)

```
Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return [1,3,3,1].

Note:
Could you optimize your algorithm to use only O(k) extra space?
```

```java
public class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> result = new ArrayList<>();
        for (int i = 0; i <= rowIndex; i++) {
            for (int j = i - 1; j > 0; j-- ) {       
                result.set(j, res.get(j) + res.get(j - 1));                                       
            }                                                                                    
            result.add(1);    
        }

        return result;   
    }
}
```
