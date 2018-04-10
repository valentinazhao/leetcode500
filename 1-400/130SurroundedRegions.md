[包围区域](https://leetcode.com/problems/surrounded-regions/description/)

```
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

For example,
X X X X
X O O X
X X O X
X O X X
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X
```


```java
class Solution {
    public void solve(char[][] board) {
        if(board == null || board.length == 0) 
            return;
 
        int m = board.length;
        int n = board[0].length;
 
        //merge O's on left & right boarder
        for (int i = 0; i < m; i++) {
            if (board[i][0] == 'O') {
                merge(board, i, 0);
            }
 
            if (board[i][n - 1] == 'O') {
                merge(board, i, n - 1);
            }
        }
 
        //merge O's on top & bottom boarder
        for (int j = 0; j < n; j++) {
            if (board[0][j] == 'O') {
                merge(board, 0, j);
            }
 
            if (board[m-1][j] == 'O') {
                merge(board, m - 1, j);
            }
        }
 
        //process the board
        for (int i = 0;i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                } else if (board[i][j] == '#') {
                    board[i][j] = 'O';
                }
            }
        }
    }
 
    public void merge(char[][] board, int i, int j){
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != 'O') {
            return;
        }
        
        board[i][j] = '#';
 
        merge(board, i - 1, j);
        merge(board, i + 1, j);
        merge(board, i, j - 1);
        merge(board, i, j + 1);
    }
}
````
