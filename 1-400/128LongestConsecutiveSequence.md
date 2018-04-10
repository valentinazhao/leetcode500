[求最长连续序列](https://leetcode.com/problems/longest-consecutive-sequence/description/)

```
Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given [100, 4, 200, 1, 3, 2],
The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.

Your algorithm should run in O(n) complexity.
````
O(NlogN)
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }  
        
        Arrays.sort(nums);
        
        int len = 1, result = 1, prev = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[i - 1]) {
                if (nums[i] == prev + 1) {
                    len ++;
                    result = Math.max(len, result);
                } else {
                    len = 1;
                }
                prev = nums[i];
            }
        }
        
        return result;
    }
}
```

O(n)
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }  
        
        Set<Integer> set = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            set.add(nums[i]);
        }
        
        int result = 1, len = 1;
        for (int num: nums) {
            if (!set.contains(num - 1)) {
                while (set.contains(num + 1)) {
                    len ++;
                    result = Math.max(result, len);
                    num += 1;
                }
                len = 1;
            }
        }
        
        return result;
    }
}
```
