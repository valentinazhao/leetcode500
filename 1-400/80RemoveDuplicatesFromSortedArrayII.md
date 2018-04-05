[从排好序的数组里去除重复](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/)

```
Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

For example,
Given sorted array nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.
```

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        int n = nums.length;
        if(n == 0 || n == 1) {
            return n;
        }
        
        int index = 0, i = 1, t = 1;
        while(i < n) {
            if (nums[index] == nums[i] && t < 2) {
                nums[++ index] = nums[i];
                t ++;
            } else if (nums[index] != nums[i]){
                nums[++ index] = nums[i];
                t = 1;
            }
            i++;
        }
        
        return index + 1;
    }
}
```
