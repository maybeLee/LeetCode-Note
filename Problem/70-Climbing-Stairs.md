## 70 Climbing Stairs

***Description***

```
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:

Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
Example 2:

Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```



首先，基数得到的结果必定是基数，偶数得到的结果必定是偶数

其次，n返回值为p，n-1返回值为q，n+1返回值必然为p+q

这么一看又可以用recursion了........

挺DP的，还蛮高级

### *My Solution I: Recursion*

```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n <= 3:
            return max(1,n)
        return self.climbStairs(n-1)+self.climbStairs(n-2)
```

#### *Result*

因为递归太多次跑崩了.........

Input 38的时候崩了



看来得用queue的方式代替recursion

### *My Solution II*

```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        stack = [n]
        total = 0
        while stack:
            node = stack.pop(0)
            if node <= 3:
                total += max(node, 1)
                continue
            stack.append(node-1)
            stack.append(node-2)
        return total
```

#### *Result*

还是TLE？？？？？

### *My Solution III*

还是最开始的那个n-1, n-2 的思路，这次选择再开辟一个列表存之前的记录，效果好蛮多

```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        total = [1,2,3]
        if n <= 3:
            return max(1, n)
        for i in range(4, n):
            total.append(total[-2]+total[-1])
        return total[-2]+total[-1]
```



#### *Result*

Runtime: 16 ms, faster than 71.85% of Python online submissions for Climbing Stairs.

Memory Usage: 11.8 MB, less than 34.38% of Python online submissions for Climbing Stairs.



时间上okay 但是memory还是占用了太多(我就多用了一个list啊.....小声BB)



### *Solution from LeetCode: Fibonacci Number*

> ###  In the above approach we have used $dp$ array where $dp[i]=dp[i-1]+dp[i-2]$. It can be easily analysed that $dp[i]$ is nothing but $i^{th}$ Fibonacci number.
>
> $Fib(n)=Fib(n-1)+Fib(n-2)$
>
> Now we just have to find $n^{th}$ number of the Fibonacci series having 11 and 22 their first and second term respectively, i.e. $Fib(1)=1$ and $Fib(2)=2$.

斐波那契？

```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        #Solution 2, refine the memory problem from Solution 1
        if n == 1:
            return 1
        first = 1
        second = 2
        for i in range(3,n+1):
            third = first + second
            first = second
            second = third
        return second
```

确实，在我的Solution III里面，尽管创建了一个list，也只用了list末尾的两个数，因此用这种方法能够有效地缓解内存问题



#### *Result*

Runtime: 8 ms, faster than 98.03% of Python online submissions for Climbing Stairs.

Memory Usage: 11.8 MB, less than 32.81% of Python online submissions for Climbing Stairs.



为什么时间上面能够他妈的这么顶？(可能是因为最后一个solution就是最简单的赋值，solution III还加上了列表的一些zz运算)

all right