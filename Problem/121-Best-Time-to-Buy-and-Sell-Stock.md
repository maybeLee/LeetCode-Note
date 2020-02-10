## 121 Best Time to Buy and Sell Stock

```
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

Example 1:

Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
Example 2:

Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```



### *My Solution I: Brute Force*

两个for 循环

#### *Code*

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        #Solution 1 Brutal for*2
        max_prices = 0
        for i in range(len(prices)-1):
            for j in range(i+1, len(prices)):
                if (prices[j] - prices[i]) > max_prices:
                    max_prices = prices[j] - prices[i]
        return max_prices
```



### *Another Solution*



If we plot the numbers of the given array on a graph, we get:

![Profit Graph](https://leetcode.com/media/original_images/121_profit_graph.png)

The points of interest are the peaks and valleys in the given graph. We need to find the largest peak following the smallest valley. We can maintain two variables - minprice and maxprofit corresponding to the smallest valley and maximum profit (maximum difference between selling price and minprice) obtained so far respectively.



#### *Code*

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """        
        #Solution 2 Dynamic Programming? use stack
        minprice = 10000
        maxprofit = 0
        for i in range(len(prices)):
            if prices[i] < minprice:
                minprice = prices[i]
            elif prices[i] -minprice > maxprofit:
                maxprofit = prices[i] - minprice
        return maxprofit
```



#### *Result*

Runtime: 44 ms, faster than 89.86% of Python online submissions for Best Time to Buy and Sell Stock.

Memory Usage: 12.6 MB, less than 30.28% of Python online submissions for Best Time to Buy and Sell Stock.





ACTUALLY I AM THINKING MAYBE I CAN USE DYNAMIC PROGRAMMING TO ACHIEVE THIS PROBLEM, BUT I HAVEN'T FIGURE IT OUT YET