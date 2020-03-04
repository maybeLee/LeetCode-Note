## 17 Letter Combinations of a Phone Number

### *Description*

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![img](..\assets\200px-Telephone-keypad2.svg.webp)

**Example:**

```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**Note:**

Although the above answer is in lexicographical order, your answer could be in any order you want.



一个思路是解决两个字符串的组合问题，两个字符串的问题解决了，三个四个字符串就是叠加的事情了，首先需要一个list存a-z的所有字符串，然后用一个二维list存需要组合的那些字符串（感觉这个内存有一点浪费了），接着问题就化为了字符串的组合问题

如何对字符串进行组合排列：

最简单的方法就是O(n^2)的暴解法，但是之前已经O(n^2)了，再加一个O(n^2)就要爆炸了，尝试用binary方法

#### *Code*

```python
class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        def combination(string1, string2):
            ############################
            #This is a function to combin two string
            #input: list[str], list[str]
            #output: list[str]
            ############################
            returnList = []
            for i in string1:
                for j in string2:
                    returnList.append(i+j)
            return returnList     
        phone = {'2': ['a', 'b', 'c'],
                 '3': ['d', 'e', 'f'],
                 '4': ['g', 'h', 'i'],
                 '5': ['j', 'k', 'l'],
                 '6': ['m', 'n', 'o'],
                 '7': ['p', 'q', 'r', 's'],
                 '8': ['t', 'u', 'v'],
                 '9': ['w', 'x', 'y', 'z']}
        if len(digits) == 1:
            return phone[digits[0]]
        if len(digits) == 0:
            return []
        string1 = phone[digits[0]]
        for i in range(1, len(digits)):
            string2 = phone[digits[i]]
            string1 = combination(string1, string2)
        return string1
```



这个地方，之前卡住的时候是因为字符串表示的方式不对，导致两个字符串组合的时候一直绕不过来，现在换了用字典，值为list的方式表述，一下子就写出来了.....



#### *Result*

Runtime: 16 ms, faster than 79.24% of Python online submissions for Letter Combinations of a Phone Number.

Memory Usage: 11.8 MB, less than 35.71% of Python online submissions for Letter Combinations of a Phone Number.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/309263843/) | 16 ms   | 11.8 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/309263820/) | 16 ms   | 11.9 MB | python   |
| a minute ago      | [Accepted](https://leetcode.com/submissions/detail/309263660/) | 16 ms   | 11.9 MB | python   |

又是Memory很拉瓜，可能就是我声明了一个returnList的变量浪费了一点空间



### *LeetCode用了一种很zz的Backtrack方法......*

直接放代码吧，想回顾Backtrack可以戳[BackTrack](../Summary/BackTrack.md) or [39 Combination Sum](../Problem/39-Combination-Sum.md)

#### *Code*

```python
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        phone = {'2': ['a', 'b', 'c'],
                 '3': ['d', 'e', 'f'],
                 '4': ['g', 'h', 'i'],
                 '5': ['j', 'k', 'l'],
                 '6': ['m', 'n', 'o'],
                 '7': ['p', 'q', 'r', 's'],
                 '8': ['t', 'u', 'v'],
                 '9': ['w', 'x', 'y', 'z']}
                
        def backtrack(combination, next_digits):
            # if there is no more digits to check
            if len(next_digits) == 0:
                # the combination is done
                output.append(combination)
            # if there are still digits to check
            else:
                # iterate over all letters which map 
                # the next available digit
                for letter in phone[next_digits[0]]:
                    # append the current letter to the combination
                    # and proceed to the next digits
                    backtrack(combination + letter, next_digits[1:])
                    
        output = []
        if digits:
            backtrack("", digits)
        return output
```



