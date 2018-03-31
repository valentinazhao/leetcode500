[下一个排列](https://leetcode.com/problems/next-permutation/description/)

```java
public class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length;
        if (n < 2) {
            return ;
        }
        
        int i = n - 1;
        while (i >= 1 && nums[i] <= nums[i - 1]) {
            i --;
        }
        
        if (i == 0) {
            Arrays.sort(nums);
            return ;
        }
        
        int index = i;
        for (int j = i; j < n; j++) {
            if (nums[j] > nums[i - 1] && nums[j] < nums[index]) {
                index = j;
            }
        }
        
        swap(nums, i - 1, index);
        
        Arrays.sort(nums, i, n);      
        
    }
    
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```
