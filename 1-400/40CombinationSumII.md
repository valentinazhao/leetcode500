[组合总数之二](https://leetcode.com/problems/combination-sum-ii/description/)

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> tempList = new ArrayList<>();
        Arrays.sort(candidates);
        boolean[] visited = new boolean[candidates.length];
        helper(candidates, target, visited, 0, 0, tempList, res);
        return res;
    }
    private void helper(int[] candidates, int target, boolean[] visited, int sum, int start, List<Integer> tempList, List<List<Integer>> res) {
        if (sum > target) {
            
        } else if (sum == target) {
            res.add(new ArrayList(tempList));
        } else {
            for (int i = start; i < candidates.length; ++i) {
                if (i > 0 && !visited[i - 1] && candidates[i] == candidates[i - 1]) continue;
                tempList.add(candidates[i]);
                visited[i]  = true;
                helper(candidates, target, visited, sum + candidates[i], i + 1, tempList, res);
                tempList.remove(tempList.size() - 1);
                visited[i] = false;           
            }
        }
    }
}
```
