[求解数独](https://leetcode.com/problems/sudoku-solver/description/)

```java
class Solution {
    public void solveSudoku(char[][] board) {
        if (board == null || board.length == 0 || board[0].length == 0) return ;
        dfsHelper(board, 0, 0);
    }
    
    private boolean dfsHelper(char[][] board, int i, int j) {
        // Base case
        while (board[i][j] != '.') {
            j ++; // change to next column
            if (j == 9) {
                if (i == 8) return true; 
                i ++;
                j = 0;
            }
        }
        boolean[] rowChecker = new boolean[9];
        boolean[] colChecker = new boolean[9];
        boolean[] subChecker = new boolean[9];
        
        fillCheckers(board, rowChecker, colChecker, subChecker, i, j);
        
        for (int cur = 1; cur <= 9; cur++) {
            board[i][j] = (char)(cur + '0');
            if (check(board, rowChecker, colChecker, subChecker, i, j, cur) && dfsHelper(board, i, j)) {
                return true;
            }
            board[i][j] = '.';
        }
        return false;
    }
    
    private boolean check(char[][] board, boolean[] rowChecker, boolean[] colChecker, boolean[] subChecker, int i, int j, int curr) {
        if (rowChecker[curr- 1] || colChecker[curr - 1] || subChecker[curr - 1]) {
            return false;
        }
        return true;
    }
    
    private void fillCheckers(char[][] board, boolean[] rowChecker, boolean[] colChecker, boolean[] subChecker, int row, int col) {
        // Fill row
        for (int j = 0; j < 9; j++) {
            if (board[row][j] != '.') {
                rowChecker[board[row][j] - '1'] = true;
            }
        }
        // Fill column
        for (int i = 0; i < 9; i++) {
            if (board[i][col] != '.') {
                colChecker[board[i][col] - '1'] = true;
            }
        }
        // Fill subMatrix
        int startX = row / 3, startY = col / 3;
        for (int x = startX * 3; x < startX * 3 + 3; x ++) {
            for (int y = startY * 3; y < startY * 3 + 3; y++) {
                if (board[x][y] != '.') {
                    subChecker[board[x][y] - '1'] = true;
                }
            }
        }
    }
}
```
