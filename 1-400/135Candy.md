[分糖果问题](https://leetcode.com/problems/candy/description/)

```
There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy.
Children with a higher rating get more candies than their neighbors.
What is the minimum candies you must give?
```

 
Solution 1: 两次遍历
```java
class Solution {
    public int candy(int[] ratings) {
        if (ratings == null || ratings.length == 0) {
            return 0;
        }
        
        int n = ratings.length;
        int[] nums = new int[n];
        Arrays.fill(nums, 1);
        for (int i = 1; i < n; i++) {
            if (ratings[i - 1] < ratings[i]) {
                nums[i] = nums[i - 1] + 1;
                //System.out.println("nums[i]=" + nums[i]);
            }
        }
        for (int i = n - 1; i >= 1; i--) {
            if (ratings[i] < ratings[i - 1]) {
                nums[i - 1] = Math.max(nums[i - 1], nums[i] + 1);
                //System.out.println("nums[i - 1]=" + nums[i - 1]);
            }
        }
        
        int rst = 0;
        for (int num: nums) {
            rst += num;
        }
        
        return rst;
    }
}
```

Solution 2: http://www.allenlipeng47.com/blog/index.php/2016/07/21/candy/
```
