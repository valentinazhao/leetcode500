[买卖股票最佳时间之三](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/description/)

```
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note:
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
```

```
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

Example 1:

Input: [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
             Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
Example 2:

Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
Example 3:

Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```


```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }
        
        int n = prices.length;
        int[] leftProfit = new int[n];
        
        int maxLeftProfit = 0, minPrice = prices[0];
        for (int i = 1; i < n; i++) {
            if(prices[i] < minPrice) {
                minPrice = prices[i];
            } else {
                maxLeftProfit = Math.max(maxLeftProfit, prices[i] - minPrice);
            }
            leftProfit[i] = maxLeftProfit;
        }
        
        int ret = leftProfit[n-1];
        int maxRightProfit = 0, maxPrice = prices[n - 1];
        for(int i = n - 2; i >= 0; i--) {
            if(prices[i]>maxPrice) {
                maxPrice = prices[i];
            } else {
                maxRightProfit = Math.max(maxRightProfit, maxPrice-prices[i]);
            }
            ret = Math.max(ret, maxRightProfit + leftProfit[i]);
        }
        
        return ret;
    }
}

```java
Idea is simple : Keep track of the minimum value till previous day and 
check how much maximum profit can be obtained for current day.

public int maxProfit(int[] prices) {
     if (prices == null || prices.length == 0) {
          return 0;
     }
     
     int trans = 2, n = prices.length;
     int[][] dp = new int[trans][n + 1];
     
     for (int i = 1; i <= trans; i++) {
          int min = Integer.MAX_VALUE;
	  for (int j = 1; j < n; j++) {
	  	min = Math.min(min, prices[j - 1] - dp[i - 1][j - 1]);
		dp[i][j] = Math.max(dp[i][j - 1], prices[j] - min);
	  }
     }
     
     return dp[trans][n - 1];
}
```
