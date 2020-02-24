## 62 Unique Paths

### *Description*

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![img](../assets/robot_maze.png)
Above is a 7 x 3 grid. How many possible unique paths are there?

**Note:** *m* and *n* will be at most 100.

**Example 1:**

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```

**Example 2:**

```
Input: m = 7, n = 3
Output: 28
```



这就是个排列组合问题啊，比如说7x3的地图，机器人需要右移6次，下移2次，假设右移为0，下移为1，那么就是6个0和2个1的排列组合，可不可以用backtrack？



### *My Solution: Recursion*

无脑递归

#### *Code*

```python
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        def findPaths(m, n):
            if m*n == 0:
                return 1
            return findPaths(m-1, n)+findPaths(m, n-1)
        return findPaths(m-1,n-1)
```



#### *Result*

TLE...........

多的方法我不会了.......先做其他的吧



### *My Solution II Dynamic Programming*

这个方法是 [64 Minimum Path Sum](../Problem/64-Minimum-Path-Sum.md)这一道题得到的思路，感觉自己动态规划的理解都有错误，动态规划不是简单的递归，需要用额外的内存存东西的啊



拿一个数组存，到每一个单元能有多少路，然后下一个单元就是两条路径加起来，woc真的简单

#### *Code*

```python
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        #Solution II Dynamic Programming
        dp = [[0 for i in range(m)] for j in range(n)]
        assert len(dp) == n and len(dp[0]) == m, "size of dp is wrong"
        for i in range(m):
            dp[0][i] = 1
        for i in range(n):
            dp[i][0] = 1
        for i in range(1, n):
            for j in range(1, m):
                dp[i][j] = dp[i-1][j]+dp[i][j-1]
        return dp[-1][-1]
```

需要注意的是：m表示列的个数，n表示行的个数，别弄反了



#### *Result*

Runtime: 16 ms, faster than 80.52% of Python online submissions for Unique Paths.

Memory Usage: 11.7 MB, less than 75.86% of Python online submissions for Unique Paths.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/306406261/) | 16 ms   | 11.7 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/306406225/) | 20 ms   | 11.6 MB | python   |

很开心！！！