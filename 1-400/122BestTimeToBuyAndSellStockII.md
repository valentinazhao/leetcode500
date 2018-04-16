[买卖股票最佳时间之二](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

```
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
```

finding all ascending sequences
```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }
        
        int i = 0, n = prices.length, result = 0;
        while (i < n) {
            int j = i;
            while (j + 1< n && prices[j] <= prices[j + 1]) {
                j ++;
            }
            result += prices[j] - prices[i];
            i = j + 1;
        }
        
        return result;
    }
}
```
