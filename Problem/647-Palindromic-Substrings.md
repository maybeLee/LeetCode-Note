## 647 Palindromic Substrings

### *Description*

```
Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

Example 1:

Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
 

Example 2:

Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
 

Note:

The input string length won't exceed 1000.
```



在一个大字符串里面找回文子字符串，这道题目我真的木有想法....



### *Solution from LeetCode*

这个答案很巧妙的将注意力集中在了回文的中心点，有两种可能，如果回文是奇数的话，中心点就是一个元素，如果回文是偶数的话，中心点是两个元素之间

还有一个特点就是：一个大回文里面共用相同中心点的小子字符串必定是回文字符串

#### *Code*

```python
class Solution(object):
    def countSubstrings(self, s):
        """
        :type s: str
        :rtype: int
        """
        N = len(s)
        ans = 0
        for center in xrange(2*N - 1):
            left = center / 2
            right = left + center % 2
            while left >= 0 and right < N and s[left] == s[right]:
                ans += 1
                left -= 1
                right += 1
        return ans
```



#### *Result*

Runtime: 88 ms, faster than 90.04% of Python online submissions for Palindromic Substrings.

Memory Usage: 11.8 MB, less than 50.00% of Python online submissions for Palindromic Substrings.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/303805727/) | 88 ms   | 11.8 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/303805719/) | 92 ms   | 11.8 MB | python   |
| 3 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/303805338/) | 88 ms   | 11.9 MB | python   |



真是个好方法......