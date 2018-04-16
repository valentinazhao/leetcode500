[二和之三-数据结构设计](https://leetcode.com/problems/two-sum-iii-data-structure-design/description/)


```
Design and implement a TwoSum class. It should support the following operations: add and find.

add - Add the number to an internal data structure.
find - Find if there exists any pair of numbers which sum is equal to the value.

For example,
add(1); add(3); add(5);
find(4) -> true
find(7) -> false
```


```
这题easy难度，我就用arraylist + sort一次bug free完了。

But, 这个帖子说的很好 https://leetcode.com/problems/two-sum-iii-data-structure-design/discuss/52005/Trade-off-in-this-problem-should-be-considered 

“The big data test only have the condition that lots of add and few find. In fact, there has to be one operation’s time 
complexity is O(n) and the other is O(1), no matter add or find. So clearly there’s trade off when solve this problem, 
prefer quick find or quick add.
If consider more find and less add or we only care time complexity in finding.For example, add operation can be pre-done.”

以下是code

```


```java
public class TwoSum {
    Map<Integer,Integer> hm;
    
    TwoSum(){
        hm = new HashMap<Integer,Integer>();
    }
    // Add the number to an internal data structure.
	public void add(int number) {
	    if(hm.containsKey(number)){
	        hm.put(number,2);
	    }else{
	        hm.put(number,1);
	    }
	}

  // Find if there exists any pair of numbers which sum is equal to the value.
	public boolean find(int value) {
	    Iterator<Integer> iter = hm.keySet().iterator();
	    while(iter.hasNext()){
	        int num1 = iter.next();
	        int num2 = value - num1;
	        if(hm.containsKey(num2)){
	            if(num1 != num2 || hm.get(num2) == 2){
	                return true;
	            }
	        }
	    }
	    return false;
	 }
}
