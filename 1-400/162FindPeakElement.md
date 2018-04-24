[求数组的局部峰值](https://leetcode.com/problems/find-peak-element/description/)


```
A peak element is an element that is greater than its neighbors.

Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num[-1] = num[n] = -∞.

For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.

click to show spoilers.

Note:
Your solution should be in logarithmic complexity.
```

二分大法
```
Most people have figured out the binary search solution but are not able to understand how its working. 

I will try to explain it simply. What we are essentially doing is going in the direction of the rising slope

(by choosing the element which is greater than current). How does that guarantee the result? Think about it, there are 2 

possibilities.a) rising slope has to keep rising till end of the array b) rising slope will encounter a lesser element and

go down.

In both scenarios we will have an answer. In a) the answer is the end element because we take the boundary as -INFINITY b) 

the answer is the largest element before the slope falls. Hope this makes things clearer.
```


更新：写的太丑了
```java
public class Solution {
    public int findPeakElement(int[] nums) {
        int n = nums.length;
        
        int l = 0, r = n - 1;
        while (l < r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] < nums[mid + 1]) {
                l = mid + 1;
            } else {
                r = mid;
            }
        }
        
        return l;
    }
}
```
