[子集之二](https://leetcode.com/problems/subsets-ii/description/)

```
Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,2], a solution is:

[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> tmpList = new ArrayList<>();
        helper(nums, 0, res, tmpList);
        return res;
    }
    
    private void helper(int[] nums, int pos, List<List<Integer>> res, List<Integer> tmpList) {
        if(pos <= nums.length) {
            res.add(new ArrayList<>(tmpList));
        }
        
        for(int i = pos; i < nums.length; i++) {
            if(i > pos && nums[i] == nums[i-1]) continue;   
            tmpList.add(nums[i]);
            helper(nums, i + 1, res, tmpList);
            tmpList.remove(tmpList.size() - 1);
        }
    }

}
```
