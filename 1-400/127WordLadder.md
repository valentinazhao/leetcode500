[词语阶梯](https://leetcode.com/problems/word-ladder/description/)

```
Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

Only one letter can be changed at a time.
Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
For example,

Given:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]
As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.

Note:
Return 0 if there is no such transformation sequence.
All words have the same length.
All words contain only lowercase alphabetic characters.
You may assume no duplicates in the word list.
You may assume beginWord and endWord are non-empty and are not the same.
```

```java
public class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> words) {        
        Set<String> wordList = new HashSet<>(words);
        //buildMap
        Map<String, List<String>> map = new HashMap<>();
        wordList.add(beginWord);
        for (String str: wordList) {
            List<String> sub = buildList(wordList, str);
            map.put(str, sub);
        }
        //System.out.println(map.get("hit"));
        
        // BFS
        int dist = 1;
        Queue<String> q = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        q.offer(beginWord);
        visited.add(beginWord);
        
        while (!q.isEmpty()) {
            int num = q.size();
            for (int t = 0; t < num; t++) {
                String s = q.poll();
                if (s.equals(endWord)) {
                    return dist;
                }
                List<String> currLevel = map.get(s);
                for (String curr: currLevel) {
                    if (!visited.contains(curr)) {
                        q.offer(curr);
                        visited.add(curr);
                    }
                }
            }
            dist ++;
        }
        
        return 0;
    }
    private List<String> buildList(Set<String> wordList, String str) {
      List<String> res = new LinkedList<>();
        
      for (int t = 0; t < str.length(); t++) {
          StringBuilder sb = new StringBuilder(str);
          char curr = str.charAt(t);
          for (char c = 'a'; c <= 'z'; c++) {
            if (c != curr) {
                sb.setCharAt(t, c);
                //System.out.println("temp=" + curr + ",nb=" + sb.toString());
                if (wordList.contains(sb.toString())) {
                    res.add(sb.toString());
                }
            }
          }
      }
      
      return res;
    }
    ````
}
