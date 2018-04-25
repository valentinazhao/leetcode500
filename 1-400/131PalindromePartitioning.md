[拆分回文串](https://leetcode.com/problems/palindrome-partitioning/description/)

```
Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

For example, given s = "aab",
Return

[
  ["aa","b"],
  ["a","a","b"]
]
```
```
在哪里切 + 切几刀?
Time: O(2^n)
Space: O(n*2^n)

```

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> ans = new ArrayList<>();
        List<String> temp = new ArrayList<>();
        backtrack(ans, temp, s, 0);
        return ans;
    }
    
    public void backtrack(List<List<String>> ans, List<String> temp, String s, int index) {
        if(index == s.length()) {
            ans.add(new ArrayList<String>(temp));
        } else {
            for (int i = index; i < s.length(); i++) {
                if(isPalindrome(s, index, i)) {
                    temp.add(s.substring(index,i+1));
                    backtrack(ans,temp,s,i+1);
                    temp.remove(temp.size()-1);
                }
            }
        }
    }
    
    public boolean isPalindrome(String s,int i,int j) {
        while (i < j) {
            if(s.charAt(i++)!=s.charAt(j--)) {
                return false;
            }
        }
        return true;
    }
}
```
