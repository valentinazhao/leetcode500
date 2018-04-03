[有效数独](https://leetcode.com/problems/valid-sudoku/description/)

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        int n = board.length, m = board[0].length;
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (board[i][j] != '.') {
                    if (checkRow(board, i, j) || checkCol(board, i, j) || checkSub(board, i, j)) {
                        return false;
                    }
                }
            }
        }
        return true;
    }
    private boolean checkRow(char[][] board, int i, int j) {
        for (int idx = 0; idx < board[0].length; idx++) {
            if (idx != j) {
                if (board[i][idx] == board[i][j]) return true;
            }
        }
        return false;
    }
    private boolean checkCol(char[][] board, int i, int j) {
        for (int idx = 0; idx < board.length; idx++) {
            if (idx != i) {
                if (board[idx][j] == board[i][j]) return true;
            }
        }
        return false;
    }
    private boolean checkSub(char[][] board, int i, int j) {
        int row = i / 3, col = j / 3;
        for (int x = row * 3; x < (row + 1) * 3; x++) {
            for (int y = col * 3; y < (col + 1) * 3; y++) {
                if (i != x && j != y) {
                    if (board[i][j] == board[x][y]) return true;
                }
            }
        }
        return false;
    }
}
```
