## 309 Best Time to Buy and Sell Stock with Cooldown

### *Description*

```
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)
Example:

Input: [1,2,3,0,2]
Output: 3 
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```

姊妹题：[121 Best Time to Buy and Sell Stock](../Problem/121-Best-Time-to-Buy-and-Sell-Stock.md)





对于动态规划里面状态dp数组的理解

在一般的动态规划中，dp[i]表示的意思是，对于第i个采取行动得到的profit是多少，比如[抢劫题](../Problem/198-House-Robber.md)中，dp[i]表示抢第i个房子的profit是多少，这类问题用动态规划比较直观，因为它只有一个行为，抢还是不抢。

但是这道题目为什么比较难呢，因为采取的动态一共有三种，买、卖还是cooldown，cooldown就是不作为，可以忽视，即，采取的动态为：买还是卖，因此特别会举一反三的人（可惜我不是这类人）会想到用两个动态数组来存这两个状态，即，buy[i], sell[i]

下面是Lucifer 大神的思路：



## 思路

这是一道典型的 DP 问题， DP 问题的核心是找到状态和状态转移方程。

这道题目的状态似乎比我们常见的那种 DP 问题要多，这里的状态有 buy sell cooldown 三种，
我们可以用三个数组来表示这这三个状态，buy,sell, cooldown.

- buy[i]表示第 i 天，且以 buy 结尾的最大利润
- sell[i]表示第 i 天，且以 sell 结尾的最大利润
- cooldown[i]表示第 i 天，且以 sell 结尾的最大利润

我们思考一下，其实 cooldown 这个状态数组似乎没有什么用，因此 cooldown 不会对`profit`产生
任何影响。 我们可以进一步缩小为两种状态。

- buy[i] 表示第 i 天，且以 buy 或者 cooldown 结尾的最大利润
- sell[i] 表示第 i 天，且以 sell 或者 cooldown 结尾的最大利润

对应的状态转移方程如下：

> 这个需要花点时间来理解

```
  buy[i] = Math.max(buy[i - 1], sell[i - 2] - prices[i]);
  sell[i] = Math.max(sell[i - 1], buy[i - 1] + prices[i]);
```

我们来分析一下，buy[i]对应第 i 的 action 只能是 buy 或者 cooldown。

- 如果是 cooldown，那么 profit 就是 buy[i - 1]
- 如果是 buy，那么就是`前一个卖的profit减去今天买股票花的钱`，即 sell[i -2] - prices[i]

> 注意这里是 i - 2，不是 i-1 ，因为有 cooldown 的限制

sell[i]对应第 i 的 action 只能是 sell 或者 cooldown。

- 如果是 cooldown，那么 profit 就是 sell[i - 1]
- 如果是 sell，那么就是`前一次买的时候获取的利润加上这次卖的钱`，即 buy[i - 1] + prices[i]

## 关键点解析

- 多状态动态规划



#### *My Code*

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) <= 1:
            return 0
        buy_i_1 = max(-prices[1], -prices[0])
        sell_i_2 = 0
        sell_i_1 = max(0, -prices[0] + prices[1])
        for i in range(2, len(prices)):
            buy_i_1 = max(buy_i_1, sell_i_2 - prices[i])
            sell_i_2 = sell_i_1
            sell_i_1 = max(sell_i_1, buy_i_1 + prices[i])
        return max(buy_i_1, sell_i_1)
```

这个代码我写得很满意！！！！！

#### *Result*

Runtime: 24 ms, faster than 83.43% of Python online submissions for Best Time to Buy and Sell Stock with Cooldown.

Memory Usage: 12.1 MB, less than 23.08% of Python online submissions for Best Time to Buy and Sell Stock with Cooldown.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/309244281/) | 24 ms   | 12.1 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/309244258/) | 24 ms   | 12.1 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/309244185/) | 20 ms   | 12 MB   | python   |



为啥内存会这么坑？我这是O(1)的额外内存啊........

要直接在prices上面修改吗？