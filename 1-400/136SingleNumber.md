[单独的数字](https://leetcode.com/problems/single-number/description/)

```
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
```


由于数字在计算机是以二进制存储的，每位上都是0或1，如果我们把两个相同的数字异或，0与0异或是0,1与1异或也是0，那么我们会得到0。根据这个特点，我们把数组中所有的数字都异或起来，则每对相同的数字都会得0，然后最后剩下来的数字就是那个只有1次的数字
````java
public class Solution {
    public int singleNumber(int[] nums) {
        int x = 0;
        for (int num: nums) {
		        x = x ^ num;
        }
	      return x;
    }
}
