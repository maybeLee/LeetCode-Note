## 64 Minimum Path Sum

### *Description*

```
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example:

Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```



动态规划？！

### *My Solution I Dynamic Programming*

每一个单元最多由两个单元走过来，因此只用比较到达这前两个代码的最短路径就好

#### *Code*

```python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        #Solution: Dynamic Programming
        def findmin(x,y,grid):
            if x == 0 and y != 0:
                return findmin(x,y-1,grid)+grid[x][y]
            elif y == 0 and x != 0:
                return findmin(x-1,y,grid)+grid[x][y]
            elif x == 0 and y == 0:
                return grid[x][y]
            return min(findmin(x-1,y, grid),findmin(x,y-1, grid))+grid[x][y]
        m = len(grid)
        n = len(grid[0])
        return findmin(m-1, n-1, grid)
```



#### *Result*

TLE........



### *My Solution II: Backtrack*

这个跟DP一样的啊，一个是从前往后，一个是从后往前.......



### *Solution from LeetCode*

他也是用DP做的，但是并没有用迭代的方法，而是用循环做的，创建一个矩阵存储之前的值，这种方法很好诶.....我之前recursion用了很多重复没用的递归的

代码可以学习一下：

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        r = len(grid)
        c = len(grid[0])
        
        dp = grid.copy()
        
        for i in range(1, c):     # fill first row of dp
            dp[0][i] = dp[0][i-1] + grid[0][i]
        for i in range(1, r):       #fill first column of dp
            dp[i][0] = dp[i-1][0] + grid[i][0]
            
        for i in range(1, r):
            for j in range(1, c):
                dp[i][j] = min(dp[i-1][j]+grid[i][j], dp[i][j-1]+grid[i][j])
                
        return dp[-1][-1]
```



#### *Result*

Runtime: 76 ms, faster than 92.61% of Python online submissions for Minimum Path Sum.

Memory Usage: 12.9 MB, less than 41.18% of Python online submissions for Minimum Path Sum.



| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/306403758/) | 84 ms   | 12.9 MB | python   |
| a minute ago      | [Accepted](https://leetcode.com/submissions/detail/306403578/) | 76 ms   | 12.9 MB | python   |
| 12 minutes ago    | [Accepted](https://leetcode.com/submissions/detail/306401920/) | 100 ms  | 14.3 MB | python3  |

