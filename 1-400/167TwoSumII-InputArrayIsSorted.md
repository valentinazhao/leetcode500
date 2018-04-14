[二和之二-输入数组已排好序](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)


```
Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution and you may not use the same element twice.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
```


```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int n = numbers.length; 
        int left  = 0, right = n - 1; 
          
        while (left < right) {
            int tmp = numbers[left] + numbers[right];
            if (tmp == target) {
                return new int[]{left + 1, right + 1};
            } else if (tmp < target) {
                left++;
            } else {
                right--;
            }
         
        return null;
    }
}
```
