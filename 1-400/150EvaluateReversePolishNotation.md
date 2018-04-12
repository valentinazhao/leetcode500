[计算逆波兰表达式](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)

```
Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are +, -, *, /. Each operand may be an integer or another expression.

Some examples:

  ["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9
  ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6
```

逆波兰表达式就是把操作数放前面，把操作符后置的一种写法
```java
public class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<Integer>();
  
        for (int i = 0; i < tokens.length; i++) {
            switch (tokens[i]) {
            case "+":
                stack.push(stack.pop() + stack.pop());
                break;
          
            case "-":
                stack.push(-stack.pop() + stack.pop());
                break;
          
            case "*":
                stack.push(stack.pop() * stack.pop());
                break;

            case "/":
                int n1 = stack.pop(), n2 = stack.pop();
                stack.push(n2 / n1);
                break;
          
            default:
                stack.push(Integer.parseInt(tokens[i]));
            }
        }
  
        return stack.pop();
    }
}
```
