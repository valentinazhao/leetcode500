[产生括号](https://leetcode.com/problems/generate-parentheses/description/)

```java
class Solution {  
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        helper(n, n, new StringBuilder(""), result);
        return result;
    }
    public void helper(int left, int right, StringBuilder sb, List<String> result) {
        if (left < 0 || right < 0 || left > right) {
            return ;
        }
        if (left == 0 && right == 0) {
            result.add(new String(sb.toString()));
            return ;
        }
        
        sb.append('(');
        helper(left - 1, right, sb, result);
        sb.deleteCharAt(sb.length() - 1);
        
        sb.append(')');
        helper(left, right - 1, sb, result);
        sb.deleteCharAt(sb.length() - 1);
    }
}
```
