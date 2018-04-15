[最接近的三数之和](https://leetcode.com/problems/3sum-closest/description/)

```java
public class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if (nums == null || nums.length < 3) {
            return 0;    
        } 
    
        Arrays.sort(nums);
        int best = Math.abs(nums[0] + nums[1] + nums[2] - target);
        int bestSum = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < nums.length - 2; i ++) {
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                int tmp = Math.abs(sum - target);
            
                if (tmp < best) {
                    best = tmp;
                    bestSum = sum;
                }
            
                if (sum < target) {
                    left ++;    
                } else {
                    right --;
                }
            }
        }
        
        return bestSum;
    }
}
```
