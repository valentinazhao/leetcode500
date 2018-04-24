[买卖股票最佳时间之四](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/description/)

```
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most k transactions.

Note:
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

```
dp[i][j] means max profit at day j with at most i transactions.

so there are two possible situations on day j:

do nothing on day j, which means at most i transactions are all done before day j, so dp[i][j] = dp[i][j-1]

sell at price[j], which means before day j there will be at most i-1 transactions.

and because you sell the stock on day j, you must have already bought it before day j.the last time you bought it before day j 
could be any day between [0, j-1].

let's say the last time you bought it on day jj, where jj is in range [0, j-1].

in this case you didn't touch price[jj] before you bought it. so what's the max profit before you bought it on day jj, well 
obviously it's dp[i-1][jj-1]. it's also dp[i-1][jj] because in this case you can only buy it on day jj and to keep the profit 
maximum you will do nothing on day jj.

after all you bought it on day jj and the "max profit" becomes max(dp[i-1][jj] - prices[jj]), this isn't the max profit on 
day jj with at most i-1 transaction, this is the max profit where you already bought the stock on day jj with at most i 
transactions.

```




```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        if (prices == null || prices.length == 0 || k == 0) {
            return 0;
        }
        
        int n = prices.length;
        if (k >= n / 2) return quickSolve(prices);
        
        int[][] dp = new int[k + 1][n + 1];     
        for (int i = 1; i <= k; i++) {
            int min = Integer.MAX_VALUE;
            //  [     合成一个   ]        
            // [1, 2, 4, 2, 5, 7, 2, 4, 9]
            for (int j = 1; j < n; j++) {
                min = Math.min(min, prices[j - 1] - dp[i - 1][j - 1]);
                dp[i][j] = Math.max(dp[i][j - 1], prices[j] - min);
            }  
        }
        
        return dp[k][n - 1];
    }
    private int quickSolve(int[] prices) {
        int len = prices.length, profit = 0;
        for (int i = 1; i < len; i++)
            // as long as there is a price gap, we gain a profit.
            if (prices[i] > prices[i - 1]) profit += prices[i] - prices[i - 1];
        return profit;
    }
}
```
