[复原IP地址](https://leetcode.com/problems/restore-ip-addresses/description/)

```
Given a string containing only digits, restore it by returning all possible valid IP address combinations.

For example:
Given "25525511135",

return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)
```

```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<>();
        List<String> tmpList = new ArrayList<>();
        helper(res, tmpList, s, 0, "0");
        
        return res;
    }
    public void helper (List<String> res, List<String> tmpList, String s, int start, String temp) {
    	if (tmpList.size() > 4 || Integer.parseInt(temp) > 255 || (temp.charAt(0) == '0' && temp.length() != 1)) {
    		return;
    	} else if (tmpList.size() == 4 && start == s.length()) {
            StringBuilder sb = new StringBuilder("");
            for(String e: tmpList) {
                sb.append(e + ".");
            }
            res.add(sb.substring(0, sb.length() - 1));
            return;
        }
        
        for (int i = 1; i < 4; i++) {
        	if((start + i) > s.length()) {
            	return;
            }
        	//System.out.println("substring: " + s.substring(start, start + i) + " start = " + start + " i = " + i);
            String tmp = s.substring(start, start + i);
            tmpList.add(tmp);
            helper(res, tmpList, s, start + i, tmp);
            tmpList.remove(tmpList.size() - 1);
        }
    }
}
```
