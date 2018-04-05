[组合项](https://leetcode.com/problems/combinations/description/)

```
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:

[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> tmpList = new ArrayList<>();
        helper(n, k, 1, res, tmpList);
        return res;
    }
    public void helper(int n, int k, int start, List<List<Integer>> res, List<Integer> tmpList) {
        if(tmpList.size() == k) {
            res.add(new ArrayList<>(tmpList));
            return ;
        }
        if (tmpList.size() > k) {
            return ;
        }
        for(int i = start; i <= n; i++) {
            /*if(tmpList.contains(i)) {
                continue;
            }*/
            tmpList.add(i);
            helper(n, k, i + 1, res, tmpList);
            tmpList.remove(tmpList.size() - 1);
        }
    }
}
```
