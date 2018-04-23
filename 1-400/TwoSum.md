[两数之和](https://leetcode.com/problems/two-sum/description/)


```
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```


Solution 1 - Time: O(nlogn) Space: O(1)
```java

如果返回值只是boolean，可以用sort的方法，如果返回的是Index,sort会打乱顺序的。
```


Solution 2 - Time: O(n) Space: O(n)
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        if (nums == null || nums.length == 0) {
            return result;
        }
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int number = nums[i];
            if (map.containsKey(nums[i])) {
                result[0] = map.get(nums[i]);
                result[1] = i;
                return result;
            } else {
                map.put(target - nums[i], i);
            }
            
        }
        return result;
    }  
}
```
