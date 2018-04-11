[拆分词句](https://leetcode.com/problems/word-break/description/)

```
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

For example, given
s = "leetcode",
dict = ["leet", "code"].

Return true because "leetcode" can be segmented as "leet code".
```

DP 
```java
public class Solution {
    public boolean wordBreak(String s, List<String> dict) {
        int n = s.length();
        boolean[] checked = new boolean[n + 1];
        checked[0] = true;
        
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                String sub = s.substring(j, i);
                if (dict.contains(sub) && checked[j]) {
                    checked[i] = true;
                    break;
                }
            }
        }
        
        return checked[n];
    }
}
```

DFS
```java
public class Solution {
    public boolean wordBreak(String s, List<String> dict) {
        // DFS
        Set<Integer> checked = new HashSet<Integer>();
        return dfs(s, 0, dict, checked);
    }
    
    private boolean dfs(String s, int index, List<String> dict, Set<Integer> set) {
        // base case
        if(index == s.length()) return true;
        // check memory
        if(set.contains(index)) return false;
        // recursion
        for(int i = index; i < s.length(); i++) {
            String t = s.substring(index, i + 1);
            if(dict.contains(t)) {
                if(dfs(s, i + 1, dict, set)) {
                    return true;
                } else {
                    set.add(i);
                }
            }
        }
        set.add(index);
        
        return false;
    }
}
```
