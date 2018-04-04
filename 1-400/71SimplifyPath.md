[简化路径](https://leetcode.com/problems/simplify-path/description/)

```
Given an absolute path for a file (Unix-style), simplify it.

For example,
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"
click to show corner cases.

Corner Cases:
Did you consider the case where path = "/../"?
In this case, you should return "/".
Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/".
In this case, you should ignore redundant slashes and return "/home/foo".

这道题让简化给定的路径，光根据题目中给的那一个例子还真不太好总结出规律，应该再加上两个例子 path = "/a/./b/../c/", => "/a/c", 
path = "/a/./b/c/", => "/a/b/c"， 这样我们就可以知道中间是"."的情况直接去掉，是".."时删掉它上面挨着的一个路径，
而下面的边界条件给的一些情况中可以得知，如果是空的话返回"/"，如果有多个"/"只保留一个. 那么我们可以把路径看做是由一个或多个"/"分割开的众多子字符串，
把它们分别提取出来一一处理即可.

```

```java
public class Solution {
    public String simplifyPath(String path) {
        Stack<String> stack = new Stack<>();
        for (String s : path.split("/")) {
            if (s.isEmpty() || s.equals(".")) {
                continue;
            }
            if (s.equals("..")) {
                if (!stack.isEmpty()) {
                    stack.pop();
                }
            } else {
                stack.push(s);
            }
        }
        
        return "/" + String.join("/", stack);
    }
}
```
