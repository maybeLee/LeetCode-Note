## 155 Min Stack

### *Description*

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





This is Silly

```python
class MinStack(object):

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.classlist = []

    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        return self.classlist.append(x)

    def pop(self):
        """
        :rtype: None
        """
        return self.classlist.pop(-1)

    def top(self):
        """
        :rtype: int
        """
        return self.classlist[-1]

    def getMin(self):
        """
        :rtype: int
        """
        return min(self.classlist)


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```



### *Result*

Runtime: 848 ms, faster than 23.42% of Python online submissions for Min Stack.

Memory Usage: 15.6 MB, less than 73.33% of Python online submissions for Min Stack.