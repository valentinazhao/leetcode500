[分数转循环小数](https://leetcode.com/problems/fraction-to-recurring-decimal/description/)


```
Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

For example,

Given numerator = 1, denominator = 2, return "0.5".
Given numerator = 2, denominator = 1, return "2".
Given numerator = 2, denominator = 3, return "0.(6)".
```


```java
class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        int sign1 = numerator > 0 ? 1 : -1, sign2 = denominator > 0 ? 1 : -1;
        long num  = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);
        long out = num / den;
        long remain = num % den;
        String result = Long.toString(out);
        if (sign1 * sign2 == -1 && (out > 0 || remain > 0)) {
            result = "-" + result;
        }
        if (remain == 0) {
            return result;
        }
        
        result += ".";
        int pos = 0;
        Map<Long, Integer> map = new HashMap<>();
        StringBuilder sb = new StringBuilder();
        while (remain != 0) {
            if (map.containsKey(remain)) {
                sb.insert(map.get(remain), "(");
                sb.append(")");
                break;
            }
            map.put(remain, pos);
            sb.append((remain * 10) / den);
            remain = (remain * 10) % den;
            pos++;
        }

        return result + sb.toString();
    }
}
```
