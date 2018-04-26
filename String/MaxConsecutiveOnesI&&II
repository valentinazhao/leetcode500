[最大连续1的个数](https://leetcode.com/problems/max-consecutive-ones/description/)

```
Given a binary array, find the maximum number of consecutive 1s in this array.

Example 1:
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
    
注意长度为1且数字为1/不为1的情况
Time: O(n) Space: O(1)
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int result = 0, len = 0;
        for (int num: nums) {
            if (num == 1) {
                len ++;
                result = Math.max(result, len);
            } else {
                len = 0;
            }
        }
        
        return result;
    }
}
```

[最大连续1的个数之二]
```
Given a binary array, find the maximum number of consecutive 1s in this array if you can flip at most one 0.

Example 1:
Input: [1,0,1,1,0]
Output: 4
Explanation: Flip the first zero will get the the maximum number of consecutive 1s.
    After flipping, the maximum number of consecutive 1s is 4.
Note:

The input array will only contain 0 and 1.
The length of input array is a positive integer and will not exceed 10,000
Follow up:
What if the input numbers come in one by one as an infinite stream? In other words, you can't store all numbers 
coming from the stream as it's too large to hold in memory. Could you solve it efficiently?
```

```
思路：
维护一个window，在这个window里面，有最多k个'0'. 最大长度就是window的右边界减去左边界.
从左到右扫描，如果碰到'0'，则加一. 这时候window里面可能出现了超过k个的'0',所以需要移动左边界. 
用while循环可以将左指针移动到合适的位置(即恰好跳过这个多余的'0'). 

完成.


```

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int l = 0, k = 1, rst = 0, cnt = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                cnt ++;
            }
            while (cnt > k) {
                if (nums[l++] == 0) {
                    cnt --;
                }
            }
            rst = Math.max(rst, i - l + 1);
        }
        
        return rst;
    }
}
```

```
Follow-up:
这种方法不合适steam，因为nums[l]要访问之前的数字. 怎么办?
可以用一个queue，将所有遇到0的位置保存下来. 这样我们就能知道l要移动到哪里了.

```

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        Queue<Integer> q = new LinkedList<>();
        int rst = 0, k = 1, l = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                q.offer(i);
            }
            if (q.size() > k) {
                l = q.peek() + 1;
                q.poll();
            }
            rst = Math.max(rst, i - l + 1);
        }
        
        return rst;
    }
}
```
