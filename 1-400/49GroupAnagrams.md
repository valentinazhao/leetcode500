[群组错位词](https://leetcode.com/problems/group-anagrams/description/)

```
Given an array of strings, group anagrams together.

For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 
Return:

[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
Note: All inputs will be in lower-case.

```

Solution one: Sorting
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> result = new ArrayList<>();
        if (strs == null || strs.length == 0) {
            return result;
        }
        
        HashMap<String, Integer> map = new HashMap<>();
        int size = 0;
        for (String str : strs) {
            char[] ch = str.toCharArray();
            // convert the str to same structure
            Arrays.sort(ch);
            String s = new String(ch);
          
            if (map.containsKey(s)) {
                List<String> list = result.get(map.get(s));
                list.add(str);
            } else {
                List<String> list = new ArrayList<>();
                list.add(str);
                map.put(s, size);
                size++;
                result.add(list);
            }
        }
        return result;   
    }
}
```
