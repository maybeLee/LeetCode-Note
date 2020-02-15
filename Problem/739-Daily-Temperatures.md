## 739 Daily Temperatures

### *Description*

```
Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.

For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].

Note: The length of temperatures will be in the range [1, 30000]. Each temperature will be an integer in the range [30, 100].
```

这道题跟406看起来很相似？最简单的方法就是两次循环咯........不管怎么样先写一下这种方法吧



### *My Easy Solution: Brute Force*

```python
class Solution(object):
    def dailyTemperatures(self, T):
        """
        :type T: List[int]
        :rtype: List[int]
        """
        #Brute Force
        hashmap = [0]*len(T)
        for i in range(len(T)):
            flag = 0
            for j in range(i+1,len(T)):
                hashmap[i] += 1
                if T[j]>T[i]:
                    flag = 1
                    break
            if flag == 0:
                hashmap[i] = 0
        return hashmap
```

#### *Result*

TLE c



### *My Solution*

I have not solution.....

### *Solution from LeetCode*

```python
class Solution(object):
    def dailyTemperatures(self, T):
        nxt = [float('inf')] * 102
        ans = [0] * len(T)
        for i in xrange(len(T) - 1, -1, -1):
            #Use 102 so min(nxt[t]) has a default value
            warmer_index = min(nxt[t] for t in xrange(T[i]+1, 102))
            if warmer_index < float('inf'):
                ans[i] = warmer_index - i
            nxt[T[i]] = i
        return ans
```



挺巧妙的......

#### *Result*

Runtime: 1020 ms, faster than 9.94% of Python online submissions for Daily Temperatures.

Memory Usage: 14.3 MB, less than 96.15% of Python online submissions for Daily Temperatures.

#### Approach #1: Next Array [Accepted]

**Intuition**

The problem statement asks us to find the next occurrence of a warmer temperature. Because temperatures can only be in `[30, 100]`, if the temperature right now is say, `T[i] = 50`, we only need to check for the next occurrence of `51`, `52`, ..., `100` and take the one that occurs soonest.

**Algorithm**

Let's process each `i` in reverse (decreasing order). At each `T[i]`, to know when the next occurrence of say, temperature `100` is, we should just remember the last one we've seen, `next[100]`.

Then, the first occurrence of a warmer value occurs at `warmer_index`, the minimum of `next[T[i]+1], next[T[i]+2], ..., next[100]`.



这道题有一个地方我应该想到的，就是既然每次都找右边的那一些，我就应该从右往左，每迭代一次就记录一次，这样即省内存又省运算时间（一边就可以）



还有一个stack的方法，希望下次我来做的时候能够想出来。