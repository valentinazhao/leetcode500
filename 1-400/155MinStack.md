[最小栈](https://leetcode.com/problems/min-stack/description/)


```
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
Example:
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```


```java
public class MinStack {

    Stack<Integer> stackData ;
    Stack<Integer> stackMin ;  // 存放到目前为止，minimum element. 所以不存在stackData弹出一个数能比stackMin栈顶元素还小.
    
    /** initialize your data structure here. */
    public MinStack() {
        stackData = new Stack<Integer>();
        stackMin = new Stack<Integer>();
    }
    
    public void push(int x) {
        if(stackMin.isEmpty()) {
            stackMin.push(x);
        }else if(stackMin.peek() >= x) {
            stackMin.push(x);
        } 
        stackData.push(x);
    }
    
    public void pop() {
        if(stackData.isEmpty()) {
            return;
        }
        int value = stackData.pop();
        if(stackMin.peek() == value) {
            stackMin.pop();
        }
    }
    
    public int top() {
        return stackData.peek();
    }
    
    public int getMin() {
        return stackMin.peek();
    }
}
```
