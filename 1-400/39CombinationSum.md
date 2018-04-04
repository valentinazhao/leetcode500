[组合总和](https://leetcode.com/problems/combination-sum/description/)

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tempList = new ArrayList<>();
        Arrays.sort(candidates);
        helper(candidates, 0, 0, target, tempList, result);
        return result;
    }
    private void helper(int[] candidates, int sum, int index, int target, List<Integer> tempList, List<List<Integer>> result) {
        if (sum == target) {
            result.add(new ArrayList<>(tempList));
            return ;
        } else if (sum > target) {
            return ;
        }
        
        for (int i = index; i < candidates.length; i++) {
            tempList.add(candidates[i]);
            helper(candidates, sum + candidates[i], i, target, tempList, result);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```
