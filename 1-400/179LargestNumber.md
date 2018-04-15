[最大组合数](https://leetcode.com/problems/largest-number/description/)


```
Given a list of non negative integers, arrange them such that they form the largest number.

For example, given [3, 30, 34, 5, 9], the largest formed number is 9534330.

Note: The result may be very large, so you need to return a string instead of an integer.
```

```
寻找next smallest number，重点是要是两个数字绑在一起不如先上单个数字大，比如[31,3] 331比313大. 也就是说两数相比，只要有一位数比两一个数小，
就应该选另外那个数。所以这道题是搞清楚各数之间的优先级，比如3比30优先级高，30比34优先级高，34比5优先级低..那么，优先级是如何判定的呢？
如果两数字位数相同，则直接比较大小.不同位则按上面的方法去判定. 这样我们能得到优先级table[4,5,3,2,1](数字小的代表优先级高). 完. 

````
这题原来是个暴力解...这题有个很无聊的 corner case : [0,0] ...

```java
class Solution {
    public String largestNumber(int[] nums) {
        PriorityQueue<String> queue = new PriorityQueue<>((a, b) -> {
        String ab = a + b;
        String ba = b + a;
        return ba.compareTo(ab);
    });
    
    for (int num : nums) {
        queue.offer(String.valueOf(num));
    }
    
    StringBuilder builder = new StringBuilder();
    while (!queue.isEmpty()) {
        builder.append(queue.poll());
    }
    
    if(builder.charAt(0) == '0') return "0"; 
    
    return builder.toString();
  }
}
```
