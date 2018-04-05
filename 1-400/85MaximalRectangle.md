[最大矩阵](https://leetcode.com/problems/maximal-rectangle/description/)

```
Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

For example, given the following matrix:

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
Return 6.
```

How to make sure the area counted is a rectangle ?
```java
public class Solution {
    public int maximalRectangle(char[][] matrix) {       
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }  
        int m = matrix.length, n = matrix[0].length;
        
        int max = 0, result = 0;
        int[] heights = new int[n];
        int[][] intMatrix = new int[m][n];
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                intMatrix[i][j] = matrix[i][j] - '0'; 
                if (intMatrix[i][j] == 0) {
                    heights[j] = 0;    
                } else {
                    heights[j] ++;
                }
            }
            max = largestRectangleArea(heights);
            result = Math.max(max, result);
        }
    
        return result;   
    }
    
    private int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<Integer>();
        int max = 0;
        int n = heights.length;
        for (int i = 0; i <= n; i++) {
            int curr = (i == n) ? -1 : heights[i];
            while (!stack.isEmpty() && curr <= heights[stack.peek()]) {
                int h = heights[stack.pop()];
                int w = (stack.isEmpty()) ? i : i - stack.peek() - 1;
                max = Math.max(max, h * w);
            }
            stack.push(i);
        }
        
        return max;
    }
}
```
