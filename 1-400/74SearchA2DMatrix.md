[搜索一个二维矩阵](https://leetcode.com/problems/search-a-2d-matrix/description/)

```
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
For example,

Consider the following matrix:

[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
Given target = 3, return true.
```
```java
public class Solution {
    public  boolean searchMatrix(int[][]matrix, int target) {
	    if (matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0) {
		    return false;
        }
        
        int m = matrix.length, n = matrix[0].length;
        int left = 0, right = m * n - 1;
        while(left + 1 < right) {
	        int mid = left + (right - left) / 2;
	        if(matrix[mid / n][mid % n] == target) {
		        return true;
            } else if (matrix[mid / n][mid % n] < target) {
	            left = mid;
            } else {
	            right = mid;
            }
        }
        
        if(matrix[right / n][right % n] == target) {
            return true;
        }
        if(matrix[left / n][left % n] == target) {
            return true;
        }

        return false;
    }
}
```
