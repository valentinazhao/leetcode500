[两个有序数组的中位数](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

```
There are two sorted arrays nums1 and nums2 of size m and n respectively.
Example:
Given A=[1,2,3,4,5,6] and B=[2,3,4,5], the median is 3.5.
Given A=[1,2,3] and B=[4,5], the median is 3.
Challenge
The overall run time complexity should be O(log (m+n)).
```
详细解释: https://www.youtube.com/watch?v=KB9IcSCDQ9k

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        // make sure  m <= n
        if (m > n) {
            return findMedianSortedArrays(nums2, nums1);
        }
        
        int k = (m + n + 1) / 2;
        int l = 0, r = m;
        
        while (l < r) {
            int m1 = l + (r - l) / 2;
            int m2 = k - m1;
            if (nums1[m1] < nums2[m2 - 1]) {
                l = m1 + 1;
            } else {
                r = m1;
            }
        }
        
        int m1 = l, m2 = k - l;
        int c1 = Math.max(m1 <= 0 ? Integer.MIN_VALUE: nums1[m1 - 1], m2 <= 0 ? Integer.MIN_VALUE: nums2[m2 - 1]);
        
        if ((m + n) % 2 == 1) {
            return c1;
        }
        int c2 = Math.min(m1 >= m ? Integer.MAX_VALUE: nums1[m1], m2 >= n ? Integer.MAX_VALUE: nums2[m2]);
        
        return (c1 + c2) * 0.5;
    }
}
```
