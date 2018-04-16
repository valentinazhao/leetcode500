[买卖股票最佳时间之三](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/description/)

```
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note:
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
```

Example: [7,9,6,1,3,2,4,7] [2,1,3,4,5,4,2,8,7]


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
