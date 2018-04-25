[Roman To Integer](https://leetcode.com/problems/roman-to-integer/description/)

先观察罗马数字转换规律. 发现：假设I,V,X,L,C级别依次升高(分别代表1,5,10,50,100)，从string后往前，如果碰上级别下降(想象成一条直线突然下降)，就减，否则加，直到又开始上升. <br>

```java
class Solution {
    public int romanToInt(String s) {
        Map<Character, Integer> map = new HashMap<>();
        map.put('I', 1);
	map.put('V', 5);
	map.put('X', 10);
	map.put('L', 50);
	map.put('C', 100);
	map.put('D', 500);
	map.put('M', 1000);
        
        // String: XCIV Decimal: 94 = -10+100-1+5
    	int number = 0, prev = -1;
	for (int i = s.length() - 1; i >= 0; i--) {
		char ch = s.charAt(i);
		int value = map.get(ch);
		if (prev == -1 || prev <= value) {
			number = number + value;
		} else {
			number = number - value;
		}
		prev = value;
	}
	return number;
    }
}
```
