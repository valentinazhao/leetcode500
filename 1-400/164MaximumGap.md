[最大间距](https://leetcode.com/problems/maximum-gap/description/)


```
Given an unsorted array, find the maximum difference between the successive elements in its sorted form.

Try to solve it in linear time/space.

Return 0 if the array contains less than 2 elements.

You may assume all elements in the array are non-negative integers and fit in the 32-bit signed integer range.

Example
Given [1, 9, 2, 5], the sorted form of it is[1, 2, 5, 9], the maximum gap is between 5and 9 = 4.

Challenge 
Sort is easy but will cost O(nlogn) time. Try to solve it in linear time and space.
```

```

Bucket sort原理参考ppt

如何知道两个数是否相邻呢? 
- 根据原理可知桶之间是有顺序的. (注意题目"successive"不等于“adjacent”!)

buckets也不一定是有序的，看这篇文章 http://www.cs.cornell.edu/courses/cs2112/2017fa/lectures/lecture.html?id=radix_sort
“Like counting sort, the time complexity is O(m + n), where m is the number of buckets and n is the length of the input array, not counting the time to sort the buckets.”
buckets sort也需要时间

```


```java
class Solution {
    public int maximumGap(int[] nums) {
        if (nums == null || nums.length <= 1) {
            return 0;
        } 
        
        int n = nums.length;
        int min = nums[0], max = nums[0];
        for (int num: nums) {
            min = Math.min(min, num);
            max = Math.max(max, num);
        }
        
        int bucket_number = (max - min) / (n - 1); // 注意n不能等于1，写在corner case里
        if (bucket_number == 0) {
            bucket_number ++;
        }
        int bucket_size = (max - min) / bucket_number + 1;
        int[] bucket_min = new int[bucket_size];
        int[] bucket_max = new int[bucket_size];
        
        //Set<Integer> set = new HashSet<>();
        for (int num: nums) {
            int idx = (num - min) / bucket_number;
            bucket_min[idx] = Math.min(bucket_min[idx], num);
            bucket_max[idx] = Math.max(bucket_max[idx], num);
            if (bucket_min[idx] == 0) {
                bucket_min[idx] = num;
            }
        }
        
        int rst = 0, prev = min;
        for (int i = 0; i < bucket_size; i++) { 
            rst = Math.max(rst, bucket_min[i] - prev);
            if (bucket_max[i] != 0) {
                prev = bucket_max[i];
            }
        }
        
        return rst;
    }
}
```
