## 394 Decode String

### *Description*

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the *encoded_string* inside the square brackets is being repeated exactly *k* times. Note that *k* is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, *k*. For example, there won't be input like `3a` or `2[4]`.

**Examples:**

```
s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```



这道题因为会出现括号里面还有括号的情况，所以用类似于递归或者循环的思想来解决比较好

首先记录有哪些bracket，然后把bracket里面的内容放到stack里面，数字的内容放到numList里面

比较难办的是存在嵌套关系，所以需要用stack

采用后进先处理的思想，对于`3[a2[c]]`的序列，首先stack构造的过程应该是：

```
Iteration 1:
  stack			      numList
|   	|			|		|
|	    |			|		|
|___a___|			|___3___|

Iteration 2:
  stack			      numList
|   	|			|		|
|___c___|			|___2___|
|___a___|			|___3___|

在第一次看到"]"后，
采用下述代码：
stack[-2] += stack[-1]*numList[-1]
stack.pop()
numList.pop()

得到结果：
  stack			      numList
|   	|			|		|
|		|			|		|
|__acc__|			|___3___|
通过栈的方法实现了嵌套字符串叠加
```



现在比较难搞的问题是，我现在默认的指示整数都是个位的，这种情况下，遇到整数就直接往numList的最后加就可以了，但是因为整数可能有多位，因此得采用标记的方式记录整数的起始和末尾，代码就写得稍微有点蠢......

#### *Code*

```python
class Solution(object):
    def decodeString(self, s):
        """
        :type s: str
        :rtype: str
        """
        stack = [""]
        number = list(str(1234567890))
        numList = []
        numStart = 0
        index = 0
        for i in range(len(s)):
            if s[i] in number:
                if numStart == 0:
                    index = i
                    numStart = 1
            elif s[i] == "[":
                stack.append("")
                numList.append(int(s[index:i]))
                numStart = 0
            elif s[i] == "]":
                stack[-2] += stack[-1]*numList[-1]
                stack.pop()
                numList.pop()
            else:
                stack[-1] += s[i]
        return stack[0]
```



#### *Result*

Runtime: 16 ms, faster than 70.25% of Python online submissions for Decode String.

Memory Usage: 11.8 MB, less than 45.10% of Python online submissions for Decode String.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307636237/) | 16 ms   | 11.8 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307636191/) | 8 ms    | 11.7 MB | python   |
| 10 minutes ago    | [Accepted](https://leetcode.com/submissions/detail/307633863/) | 16 ms   | 11.8 MB | python   |



可能是因为用了一个stack 一个list两个容器的原因，memory不太好

但是用字典的话，无法应对重复的字符串，因此暂时没有想到改进的方法

