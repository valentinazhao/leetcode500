[]()

```
Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,3], a solution is:

[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> rst = new ArrayList<>();
        List<Integer> lst = new ArrayList<>();
        if(nums.length == 0 || nums == null) {
            return rst;
        }
        helper(nums, 0, rst, lst);
        
        return rst;
    }
    
    public void helper(int[] arr, int start, List<List<Integer>> rst, List<Integer> lst) {
        rst.add(new ArrayList<>(lst));
        for(int i = start; i < arr.length; i++) {
            lst.add(arr[i]);
            helper(arr, i + 1, rst, lst);
            lst.remove(lst.size() - 1);
        }
    }
}
```
