## 20 Valid Parenthess

### *Description*

```
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

Example 1:

Input: "()"
Output: true
Example 2:

Input: "()[]{}"
Output: true
Example 3:

Input: "(]"
Output: false
Example 4:

Input: "([)]"
Output: false
Example 5:

Input: "{[]}"
Output: true
```



### *My Solution*

这道题要用栈, 类似于消消乐,两个相邻的能够匹配就消掉,如果最后能够全部消完就代表okay,不然就return false

```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        #Stack is simple, I love stack
        if s == "":
            return True
        if len(s) == 1:
            return False
        dictmap = {'(':')', '[':']', '{':'}'}
        stack = [s[0]]
        i = 1
        while True:
            stack.append(s[i])
            i += 1
            if len(stack)>1 and stack[-2] in dictmap and dictmap[stack[-2]] == stack[-1]:
                stack.pop(-1)
                stack.pop(-1)

            if i == len(s) and len(stack) != 0:
                return False
            if i == len(s) and stack == []:
                return True
```



#### *Result*

runtime很好,memory 比较差,毕竟多用了一个stack

改进方法



### *My Solution(refined)*



#### *Code*

```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        #Stack is simple, I love stack
        if s == "":
            return True
        if len(s) == 1:
            return False
        dictmap = {'(':')', '[':']', '{':'}'}
        i = 0
        s = list(s)
        while i != len(s):
            if len(s)-i-1>=1 and s[i] in dictmap and dictmap[s[i]] == s[i+1]:
                s.pop(i)
                s.pop(i)
                i -= 1
            else:
                i += 1
        if s != []:
            return False
        elif s == []:
            return True
```

大致思想是一样的,剩下的就是submit改代码找逻辑