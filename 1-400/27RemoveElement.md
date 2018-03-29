[去除元素](https://leetcode.com/problems/remove-element/description/)

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int left = 0;
        int right = nums.length - 1;
        int len = nums.length;
        while (left <= right) {
            if (nums[left] == val) {
                while (left < right && nums[right] == val) {
                    len--;
                    right--;
                }
                nums[left] = nums[right];
                right--;
                len--;
            }
            left++;
        }
        return len;
    }
}
```
