[二进制数相加](https://leetcode.com/problems/add-binary/description/)

```
Given two binary strings, return their sum (also a binary string).

For example,
a = "11"
b = "1"
Return "100".
```

```java
class Solution {
    public String addBinary(String a, String b) {        
        char[] ac = a.toCharArray();
        char[] bc = b.toCharArray();
        int ai = ac.length -1;
        int bi = bc.length -1;
        int max = Math.max(ai, bi);
        char[] result = new char[max+1];
        int sum = 0;
        while(ai >= 0 || bi >= 0) {
            if(ai >= 0) {
                sum += ac[ai--] - '0';
            }
            
            if(bi>=0) {
                sum +=bc[bi--] - '0';
            }
            
            result[max--] = (char)(sum % 2 + '0');
            sum /= 2;
        }
        
        String r = new String(result);
        if(sum == 1) {
            r = sum + r;
        }
        
        return r;
    }
}
```
