## 494 Target Sum

### *Description*

```
You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

Example 1:
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
Note:
The length of the given array is positive and will not exceed 20.
The sum of elements in the given array will not exceed 1000.
Your output answer is guaranteed to be fitted in a 32-bit integer.
```



需要注意的是，list里面的数是没有顺序关系的，比如说[1,2,3]和[1,3,2]是一样的，但是，结果始有顺序关系的

比如输入[1,0] sum = 1

输出答案应该是 2 #([1,0] and [0,1]) what the fuck



### *My Solution*

这道题一开始是想用DP做，后来发现DP会TLE

#### *Code*

```python
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        if abs(S) > sum(nums):
            return 0
        if len(nums) == 1:
            if abs(S) == nums[0]:
                if S == nums[0] == 0:
                    return 2
                else:
                    return 1
            else: 
                return 0

        return self.findTargetSumWays(nums[1:], S-nums[0]) + self.findTargetSumWays(nums[1:], S+nums[0])
```



LeetCode第一种方法也是brute force，我用把java代码转换为python 代码如下（结果还是TLE）：

```python
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        def calc(nums, i, sums, S, count):
            if i == len(nums):
                if sums == S:
                    count[0] += 1
            else:
                calc(nums, i + 1, sums + nums[i], S, count)
                calc(nums, i + 1, sums - nums[i], S, count)
        count = [0]     
        calc(nums, 0, 0, S, count)
        return count[0]
```



#### *Result*

TLE

没有办法只能根据题目特征来了.........发现以后写代码的时候不要想都不想就DP



#### *Solution II*

这道题目应该可以用二层循环做，一开始全是正的，然后一个一个减，如果遇到了sum=S的就count+=1

这样的话，似乎可以用位运算的方法，从比如说是[1,1,1,1,1]，那么组合情况就是从0b00000(0)到0b11111(31)，



这是一种想法，但是实行起来比较复杂，首先下面是brute force 二层循环的算法

#### *Code*

```

```

