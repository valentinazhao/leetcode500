[在排序矩阵中第k小的元素](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/)


```
Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

Example:

matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
Note: 
You may assume k is always valid, 1 ≤ k ≤ n2.
```


```
这题参考bittiger视频，有三种解法

其中，bs不能写成传统if(count==k)return mid;这样非常可能不存在，比如题目中例子14和13都是k=8，但14是不存在数组的。
证明为什么mid是数组中存在的数，以下
https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/discuss/85182/My-solution-using-Binary-Search-in-C++

```

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int low = matrix[0][0], high = matrix[n - 1][n - 1];
        while (low < high) {
            int mid = (low + high) / 2;
            int count = count(matrix, mid);
            if (count < k) {
                low = mid + 1;
            }else {
                high = mid;
            }
        }   
        return low;
    }
    public int count(int[][] matrix, int target) {
        int n = matrix.length - 1;
        int sum = 0, r = 0, c = n;
        while (r <= n && c >= 0) {
            if (matrix[r][c] > target) {
                c --;
            } else {
                sum += c + 1;
                r ++;
            }
        }
        return sum;
    }    
}
```

```
    从右上角开始往左往下遍历，往下means:当前数matrix[r][c]小于等于target，那么，当前行左边所有数一定符合条件，累加到sum当中，往下挪一行。
                          往左means:当前数大于target，我要尽可能往左挪，挪到第一个<= target的地方，则当前指针左边所有数一定符合条件。
                        
    同理，
    从左下角往右上bottom-up，往上means:当前数太大，我要挪到第一个<=target的行去，所以row--;
                          往右means: 当前列往上所有行的数一定小于当前行，累加到sum中去，往右挪一步，找到第一个<=target的列去。
    
    
    
    public int count(int[][] matrix, int target) {
        int n = matrix.length, r = n - 1, c = 0;
        int sum = 0;
        while (r >= 0 && c <= n - 1) {
            if (matrix[r][c] > target) r --;
            else {
                c ++;
                sum += r + 1;
            }
        }
        return sum;
    } 
```
