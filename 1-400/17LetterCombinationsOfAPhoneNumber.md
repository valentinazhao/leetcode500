[电话号码的字母组合](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

```java
class Solution {
    public List<String> letterCombinations(String digits) {
        List<String> res = new ArrayList<>();
        StringBuffer sb =  new StringBuffer();
        String[] table = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        if(digits.length() == 0 || digits == null) {
            return res;
        }
        helper(res, sb, table, digits, 0, 0);
        return res;
    }
    
    public void helper(List<String> res, StringBuffer sb, String[] table, String digits, int start, int index) {
        if (sb.length() == digits.length()) {
            res.add(sb.toString());
            return ;
        }
        char[] arr = digits.toCharArray();

        String currLevel = table[digits.charAt(index) - '0'];
        char[] curr = currLevel.toCharArray();
        for (int j = 0; j < curr.length; j++) {
            sb.append(curr[j]);
            helper(res, sb, table, digits, start + 1, index + 1);
            sb.deleteCharAt(sb.length() - 1);
        }
   }
}
```
