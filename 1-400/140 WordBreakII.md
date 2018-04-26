[拆分词句](https://leetcode.com/problems/word-break-ii/description/)

```
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. You may assume the dictionary does not contain duplicate words.

Return all such possible sentences.

For example, given
s = "catsanddog",
dict = ["cat", "cats", "and", "sand", "dog"].

A solution is ["cats and dog", "cat sand dog"].
UPDATE (2017/1/4):
The wordDict parameter had been changed to a list of strings (instead of a set of strings). Please reload the code definition to get the latest changes.
改成list以后特别容易TLE,如 "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaabaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"
                        ["a","aa","aaa","aaaa","aaaaa","aaaaaa","aaaaaaa","aaaaaaaa","aaaaaaaaa","aaaaaaaaaa"]
```

DFS https://leetcode.com/problems/word-break-ii/discuss/44287/Java-beating-95.13-with-explanation:-DFS-+-memoization-to-avoid-TLE
```java
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        List<String> res = new ArrayList<>();
        wordBreak2(s, 0, wordDict, "", new boolean[s.length() + 1], res);
        return res;
    }

    private boolean wordBreak2(String s, int left, List<String> wordDict, String prev, boolean[] invalid, List<String> res) {
        // Base case: successfully moved to the end, add result to the list.
        if (left == s.length()) {
            res.add(prev.trim());
            return true;
        }
        // whether s.substring(left) is breakable
        boolean flag = false;
        // iterate the pointer from left+1 to the end, find whether [left, i) is valid
        for (int i = left + 1; i <= s.length(); i++) {
            // if s.substring(i) is unbreakable, continue
            if (invalid[i]) {
                continue;
            }
            String sub = s.substring(left, i);
            // if substring [left,i) is valid, move on and break from i
            if (wordDict.contains(sub)) {
                flag = wordBreak2(s, i, wordDict, prev.concat(" ").concat(sub), invalid, res);
            }
        }
        // update invalid array
        invalid[left] = !flag;
        return flag;
    }
}
```

TLE method
```java
public class Solution {
    public List<String> wordBreak(String s, List<String> dict) {
        Map<Integer, List<String>> validMap = new HashMap<Integer, List<String>>();

        // initialize the valid values
        List<String> l = new ArrayList<String>();
        l.add("");
        validMap.put(s.length(), l);

        // generate solutions from the end
        for(int i = s.length() - 1; i >= 0; i--) {
            List<String> values = new ArrayList<String>();
            for(int j = i + 1; j <= s.length(); j++) {
                if (dict.contains(s.substring(i, j))) {
                    for(String word : validMap.get(j)) {
                        values.add(s.substring(i, j) + (word.isEmpty() ? "" : " ") + word);
                    }
                }
            }
            validMap.put(i, values);
        }
        return validMap.get(0);
    }
}
```

backtracking标准格式你记住了吗
```java
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        Set<String> dict = new HashSet();
        
        for(String str : wordDict)  dict.add(str);
        
        return backTrack(s, dict, new HashMap());
        
    }
    public List<String> backTrack(String s, Set<String>dict, Map<String, List<String>> memo){
        List<String> res = new ArrayList();
        if (memo.containsKey(s)) return memo.get(s);
        
        for(int i = 0; i < s.length();i++){
            String temp = s.substring(0, i + 1);
            if(dict.contains(temp)){
                if(i == s.length() - 1){
                    res.add(temp);
                }else{
                    List<String> subres = backTrack(s.substring(i + 1), dict, memo);
                    if(!subres.isEmpty()){
                        for(String str : subres){
                            res.add(temp + " " + str);                    
                        }   
                    }
                }
            }
            memo.put(s, res);
        }
             
        return res;
    }
} 
```

