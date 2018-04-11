[拆分回文串之二](https://leetcode.com/problems/palindrome-partitioning-ii/description/)

```
Given a string s, partition s such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of s.

For example, given s = "aab",
Return 1 since the palindrome partitioning ["aa","b"] could be produced using 1 cut.
```
这题cache的方法还是会TLE, 只能用DP </br>
在哪里切 + 在某处切之前最小几刀   //    [i][j]表示某段是否回文, 此处最小值如何表示 </br>
So we need two cache arraysone tracks the partition position and one tracks the number of minimum cut.
https://www.programcreek.com/2014/04/leetcode-palindrome-partitioning-ii-java/

```java
class Solution {
    public int minCut(String s) {
        int n = s.length(); 
	    boolean dp[][] = new boolean[n][n];
	    int cut[] = new int[n];
 
	    for (int j = 0; j < n; j++) {
		    cut[j] = j; //set maximum # of cut
		    for (int i = 0; i <= j; i++) {
		    	if (s.charAt(i) == s.charAt(j) && (j - i <= 1 || dp[i+1][j-1])) {
				    dp[i][j] = true;
		    		// if need to cut, add 1 to the previous cut[i-1]
			    	if (i > 0){
			    		cut[j] = Math.min(cut[j], cut[i-1] + 1);
			    	} else {
			    	// if [0...j] is palindrome, no need to cut    
	    				cut[j] = 0; 
	    			}	
	    		}
	    	}
	    }
 
    	return cut[n - 1];
    }
}
````
注： 网上包括discussion解法杂乱，多找找不同blog，找自己能理解的非常重要.
