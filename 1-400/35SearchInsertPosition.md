[搜索插入位置](https://leetcode.com/problems/search-insert-position/description/)

```java
public class Solution {
    public int searchInsert(int[] nums, int target) {
        if (nums.length == 0 || nums == null) {
            return -1;
        }
        
        int s = 0, e = nums.length;  // 去掉减一
        while (s < e) {
            int m = s + (e - s) / 2;
            if(nums[m] < target) {
                s = m + 1;
            } else {
                e = m;
            } 
           //System.out.println(" start:" + s + ", end:" + e + ", mid:" + m + ", nums[mid]:" + nums[m]);
        }
        
        return s;
    }
}
```
