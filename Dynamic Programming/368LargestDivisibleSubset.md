[最大可整除的子集合](https://leetcode.com/problems/largest-divisible-subset/description/)

```java
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        int n = nums.length;
        
        Arrays.sort(nums);
        int maxV = 0, index = -1;
        int[] prev = new int[n];
        int[] max = new int[n];
        for (int i = 0; i < n; i++) {
            max[i] = 1;
            prev[i] = -1;
            for (int j = i - 1; j >= 0; j--) {
                if (nums[i] % nums[j] == 0) {
                    if (max[j] + 1 > max[i]) {
                        max[i] = max[j] + 1;
                        prev[i] = j;
                    }
                }
            }
            if (max[i] > maxV) {
                maxV = max[i];
                index = i;
            }
        }
        
        List<Integer> res = new ArrayList<>();
        while (index != -1) {
            res.add(nums[index]);
            index = prev[index];
        }
        
        return res;
        
    }
}
```
