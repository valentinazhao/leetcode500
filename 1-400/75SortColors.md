[颜色排序](https://leetcode.com/problems/sort-colors/description/)

```
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note:
You are not suppose to use the library's sort function for this problem.

click to show follow up.

Follow up:
A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

Could you come up with an one-pass algorithm using only constant space?
```

```java
class Solution {
    public void sortColors(int[] nums) {
        int n = nums.length;
        if (nums == null || n == 0 || n == 1) {
            return ;
        }     
        
        // Where '0'/'1'/'2' start ? How many ?
        int left = 0, right = n - 1;
        for (int i = 0; i <= right; i++) {
            if (nums[i] == 0) {
                swap(nums, i, left);
                left ++;             
            } else if (nums[i] == 2) {
                swap(nums, i, right);
                right --;
                i --;
            }           
        }
    }
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```
