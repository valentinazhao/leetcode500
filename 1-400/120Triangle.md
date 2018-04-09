[三角形](https://leetcode.com/problems/triangle/description/)

```
Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.
```

注意minimum path不一定是每一行最小值！比如，[[-1],[2,3],[1,-1,-3]] 最小值-1 (-1 + 3 + -3 = -1).
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        if (triangle == null || triangle.size() == 0) {
            return Integer.MIN_VALUE;
        }   
        
        int size = triangle.size();
        if (size == 1) {
            return triangle.get(0).get(0);
        }
        int[][] dp = new int[size][size];
        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size; j++) {
                dp[i][j] = -1;
            }
        }
        return helper(triangle, 0, 0, dp);
    }
    private int helper(List<List<Integer>> list, int level, int index, int[][] dp) {
        if (dp[level][index] != -1) {
            return dp[level][index];
        }
        if (level == list.size() - 1) {
            return list.get(level).get(index);
        }
        
        dp[level][index] 
    = list.get(level).get(index) + Math.min(helper(list, level + 1, index, dp), helper(list, level + 1, index + 1, dp));
       
        return dp[level][index];
    }
}
```
