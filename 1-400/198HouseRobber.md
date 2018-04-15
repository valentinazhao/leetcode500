[怪盗基德](https://leetcode.com/problems/house-robber/description/)


```
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
```

```
这道题的本质相当于在一列数组中取出一个或多个不相邻数，使其和最大。那么我们对于这类求极值的问题首先考虑动态规划Dynamic Programming来解，
我们维护一个一位数组dp，其中dp[i]表示到i位置时不相邻数能形成的最大和，那么递推公式怎么写呢，我们先拿一个简单的例子来分析一下，
比如说nums为{3, 2, 1, 5}，那么我们来看我们的dp数组应该是什么样的，首先dp[0]=3没啥疑问，再看dp[1]是多少呢，由于3比2大，所以我们抢第一个房子的3，
当前房子的2不抢，所以dp[1]=3，那么再来看dp[2]，由于不能抢相邻的，所以我们可以用再前面的一个的dp值加上当前的房间值，和当前房间的前面一个dp值比较，
取较大值当做当前dp值，所以我们可以得到递推公式dp[i] = max(num[i] + dp[i - 2], dp[i - 1]), 由此看出我们需要初始化dp[0]和dp[1]，
其中dp[0]即为num[0]，dp[1]此时应该为max(num[0], num[1])
```



DP: dp[i] = Math.max(dp[i-1], dp[i-2]+nums[i])
```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 0) {
            return 0;
        } else if (nums.length == 1) {
            return nums[0];
        }
        int[] result = new int[nums.length];
        result[0] = nums[0];
        result[1] = Math.max(nums[0], nums[1]);
        for (int i = 2; i < nums.length; i++) {
            result[i] = Math.max(nums[i] + result[i - 2], result[i - 1]);
        }
        return result[nums.length - 1];
    }
}
```


还有一种解法，核心思想还是用DP，分别维护两个变量a和b，然后按奇偶分别来更新a和b，这样就可以保证组成最大和的数字不相邻
```java
class Solution {
    public int rob(int[] nums) {
        int prev = 0, curr = 0;
        for (int n : nums) {
            int tmp = curr;
            curr = Math.max(prev + n, curr);
            prev = tmp;
        }
        return curr;
    }
}
```
