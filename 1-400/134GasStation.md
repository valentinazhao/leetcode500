[加油站问题](https://leetcode.com/problems/gas-station/description/)

```
There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

Note:
The solution is guaranteed to be unique.
```
`
注意到这样一个现象：
1. 如果从位置i开始，i+1, i+2, i+3...一路开过来邮箱都没有空，说明什么？说明从i到i+1, i+2, i+3...肯定是正积累.
2. 现在突然发现开到位置j的时候邮箱空了，说明从i开始到j没法儿走完全程.那么，我们要从i+1开始尝试吗？不需要！为什么？因为从前面知道，位置i是正积累，
   从i+1开始走更加没办法走完i->j了,因为缺少i的正积累.同理也不需要从i+2, i+3...开始尝试.
`


```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int index = 0, sum = 0, total = 0;
        for (int i = 0; i < gas.length; i++) {
            sum += gas[i] - cost[i];
            total += gas[i] - cost[i];
            if (sum < 0) {
                index = i + 1;
                sum = 0;
            }
        }
        
        return total < 0 ? -1 : index;
    }
}
````
