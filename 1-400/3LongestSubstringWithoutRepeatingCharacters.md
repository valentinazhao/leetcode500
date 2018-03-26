[没有重复最长子字符串](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

```
Given a string, find the length of the longest substring without repeating characters.

Examples:

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. 

Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

```
###### 由于对每一个字符，只要碰到重复出现的字符就更新left，因为不能包含重复字符。每次记录下字符最后一次出现的位置。
###### m[ch] < left针对待定子字符串如果已经不包含再次出现的“重复”字符，要把当前字符囊括进去。举例，当输入字符串为"abbca"的时候，当i=4时，
###### 也就是即将要开始遍历最后一个字母a时，此时哈希表表中a对应1，b对应3，c对应4，left为2，即当前最长的子字符串的左边界为第二个b的位置，
###### 而第一个a已经不在当前最长的字符串的范围内了，那么对于i=4这个新进来的a，应该要加入结果中，而此时未被更新的哈希表中a为1，不是0，
###### 如果不判断它和left的关系的话，就无法更新结果，那么答案就会少一位，所以需要加m[s[i]] < left.

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] m = new int[256];
        int res = 0, left = 0;
        
        for (int i = 0; i < s.length(); i++) {
            int ch = s.charAt(i);
            if (m[ch] == 0 || m[ch] < left) {
                res = Math.max(res, i - left + 1);
            } else {
                left = m[ch];
            }
            m[ch] = i + 1;
        }
        
        return res;
    }
}
```
