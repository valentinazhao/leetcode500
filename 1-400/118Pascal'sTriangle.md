[帕斯卡三角形](https://leetcode.com/problems/pascals-triangle/description/)

```
Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
Return

[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

```java
public class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> rst = new ArrayList<List<Integer>>();
        if (numRows == 0) {
            return rst;
        }
        
        List<Integer> first = new ArrayList<>();
        first.add(1);
        rst.add(first);
        for (int i = 2; i <= numRows; i++) {
            List<Integer> tempList = new ArrayList<>(i);
            tempList.add(0, 1);
            tempList.add(tempList.size() - 1, 1);
            List<Integer> prev = rst.get(i - 2);
            for (int k = 1; k <= i - 2; k++) {
                tempList.add(k, prev.get(k - 1) + prev.get(k));
            }
            rst.add(new ArrayList<>(tempList));
        }
        
        
        return rst;
    }
}
```
