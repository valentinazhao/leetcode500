[序列排序](https://leetcode.com/problems/permutation-sequence/description/)

```
The set [1,2,3,…,n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

"123"
"132"
"213"
"231"
"312"
"321"
Given n and k, return the kth permutation sequence.

Note: Given n will be between 1 and 9 inclusive.
```

```java
class Solution {
    public String getPermutation(int n, int k) {
        StringBuilder sb = new StringBuilder("");
        List<Integer> arr = new ArrayList<>();
        for(int i = 1; i <= n; i++) {
            arr.add(i);
        }
        k -= 1;
        while(arr.size() != 0) {
            int index = k / factorial(n - 1);
            sb.append(Integer.toString(arr.get(index)));
            arr.remove(index);
            k = k - index * factorial(n - 1);
            n -= 1;
        }
        
        return sb.toString();
    }
    
    public int factorial(int x) {
        if (x <= 0) {
            return 1;
        }
        int sum = 1;
        for (int i = 2; i <= x; i++) {
            sum *= i;
        }
        return sum; 
    }
}
```
