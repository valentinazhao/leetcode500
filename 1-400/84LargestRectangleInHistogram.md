[直方图中的最大矩阵面积](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)

```
Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.


Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].


The largest rectangle is shown in the shaded area, which has area = 10 unit.

For example,
Given heights = [2,1,5,6,2,3],
return 10.
```

```java
public class Solution {
    public int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<Integer>(); 
        int max = 0;
        for (int i = 0; i <= heights.length; i++) {
            int currHeight = (i == heights.length) ? -1 : heights[i];
            while (!s.isEmpty() && currHeight < heights[s.peek()]) {
                int p = s.pop();
                int h = heights[p];
                int w = s.isEmpty() ? i : i - s.peek() - 1;
                max = Math.max(max, w * h);
            }
            s.push(i);
        }
        
        return max;
    }
}
```
