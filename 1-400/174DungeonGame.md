[地牢游戏](https://leetcode.com/problems/dungeon-game/description/)


```
The demons had captured the princess (P) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight (K) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons, so the knight loses health (negative integers) upon entering these rooms; other rooms are either empty (0's) or contain magic orbs that increase the knight's health (positive integers).

In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.

 

Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.

 

For example, given the dungeon below, the initial health of the knight must be at least 7 if he follows the optimal path RIGHT-> RIGHT -> DOWN -> DOWN.

-2 (K)-33-5-1011030-5 (P)
 

Notes:

 

The knight's health has no upper bound.
Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.
```

这是个in-place做法
```java
class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        int m = dungeon.length, n = dungeon[0].length;
        dungeon[m - 1][n - 1] = Math.max(1 - dungeon[m - 1][n - 1], 1);
        
        for (int i = m - 2; i >= 0; --i) {
            dungeon[i][n - 1] = Math.max(dungeon[i + 1][n - 1] - dungeon[i][n - 1], 1);
        }
        
        for (int j = n - 2; j >= 0; --j) {
            dungeon[m - 1][j] = Math.max(dungeon[m - 1][j + 1] - dungeon[m - 1][j], 1);
        }
        
        for (int i = m - 2; i >= 0; i--) {
            for (int j = n - 2; j >= 0; j--) {
                int down = Math.max(dungeon[i + 1][j] - dungeon[i][j], 1);
                int right = Math.max(dungeon[i][j + 1] - dungeon[i][j], 1);
                dungeon[i][j] = Math.min(down, right);
            }
        }
        
        return dungeon[0][0];
    }  
}
```
