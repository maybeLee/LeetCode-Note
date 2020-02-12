## 192 House Robber

### *Description*

```
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

Example 1:

Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
Example 2:

Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```

By the way, I think about dynamic programming as soon as I see the problem.

### *My Solution*

好吧我不会做，动态规划太难了，下面是从Lucifer里面copy过来的：



## 思路

这是一道非常典型且简单的动态规划问题，但是在这里我希望通过这个例子，
让大家对动态规划问题有一点认识。

为什么别人的动态规划可以那么写，为什么没有用 dp 数组就搞定了。
比如别人的爬楼梯问题怎么就用 fibnacci 搞定了？为什么？在这里我们就来看下。

思路还是和其他简单的动态规划问题一样，我们本质上在解决`对于第[i] 个房子，我们抢还是不抢。`的问题。

判断的标准就是总价值哪个更大， 那么对于抢的话`就是当前的房子可以抢的价值 + dp[i - 2]`

> i - 1 不能抢，否则会触发警铃

如果不抢的话，就是`dp[i - 1]`.

> 这里的 dp 其实就是`子问题`.

状态转移方程也不难写`dp[i] = Math.max(dp[i - 2] + nums[i - 2], dp[i - 1]);`（注：这里为了方便计算，令 `dp[0]`和 `dp[1]`都等于 0，所以 `dp[i]`对应的是 `nums[i - 2]`）

上述过程用图来表示的话，是这样的：

![198.house-robber](D:/Study/LeetCode/leetcode/assets/problems/198.house-robber.png)

我们仔细观察的话，其实我们只需要保证前一个 dp[i - 1] 和 dp[i - 2] 两个变量就好了，
比如我们计算到 i = 6 的时候，即需要计算 dp[6]的时候， 我们需要 dp[5], dp[4]，但是我们
不需要 dp[3], dp[2] ...



### *Code*

```python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        length = len(nums)
        if length == 1:
            return nums[0]
        else:
            prev = nums[0]
            cur = max(prev, nums[1])
            for i in range(2, length):
                cur, prev = max(prev+nums[i], cur), cur
            return cur
```



### *Result*

Runtime: 20 ms, faster than 54.68% of Python online submissions for House Robber.

Memory Usage: 11.9 MB, less than 10.64% of Python online submissions for House Robber.