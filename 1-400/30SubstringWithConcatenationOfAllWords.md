[串联所有单词的子串](https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/)

```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> result = new ArrayList<>();
        if (s == null || words == null || s.length() == 0 || words.length == 0) {
            return result;
        }
        
        Map<String, Integer> dict = new HashMap<>();
        for (int i = 0; i < words.length; i++) {
            if (!dict.containsKey(words[i])) {
                dict.put(words[i], 1);
            } else {
                dict.put(words[i], dict.get(words[i]) + 1);
            }
        }
        
        int m = words[0].length(), n = words.length;
        for (int i = 0; i + m * n <= s.length(); i++) {
            Map<String, Integer> map = new HashMap<>();
            int j = 0;
            while (j < n) {
                String key = s.substring(i + j * m, i + (j + 1) * m);
                if (dict.containsKey(key)) {
                    map.put(key, map.getOrDefault(key, 0) + 1);
                    if (map.get(key) > dict.getOrDefault(key, 0)) {
                        break;
                    }
                } else {
                    break;
                }
                j ++;
            }
            if (j == n) {
                result.add(i);
            }
        }
        
        return result;
    }
}
```
