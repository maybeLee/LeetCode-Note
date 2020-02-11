## 53 Maximum Subarray

### *Description*

```
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Follow up:

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
```

I won't use brute force

### *My Solution*

Still I try to just locate the start and end part, I think:

> if n[i] + n[i+1] > n[i+1]: then n[i+1] will never be the start part
>
> if n[i]+n[i-1]>n[i-1]: then n[i-1] will never be the start part

In this thought I wrote the bullshit below:

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #Okay this is my silly answer and cannot figure this out
        if len(nums) == 1:  return nums[0]
        if len(nums) == 0: return 0
        if len(nums) == 2: return max(nums[0],nums[1],sum(nums))
        start = point1 = 0
        end = point2 = len(nums)-1
        sum1 = nums[start]
        sum2 = nums[end]
        while point1<point2:
            point1 += 1
            point2 -= 1
            if sum1+nums[point1]<=nums[point1]:
                start = point1
                sum1 = nums[point1]
            else:
                sum1 += nums[point1]
            if sum2+nums[point2]<=nums[point2]:
                end = point2
                sum2 = nums[point2]
            else:
                sum2 += nums[point2]
        print(start,end)
        return sum(nums[start:end+1])
        
```

It can be find out the I wrote a lot of constraint on it, which make the code looks terrible, and I can not solve this problem using this code



### Lucifer's Solution*

#### 解法三 - 优化前缀和 - from [**@lucifer**](https://github.com/azl397985856)

我们定义函数` S(i)` ，它的功能是计算以 `0（包括 0）`开始加到 `i（包括 i）`的值。

那么 `S(j) - S(i - 1)` 就等于 从 `i` 开始（包括 i）加到 `j`（包括 j）的值。

我们进一步分析，实际上我们只需要遍历一次计算出所有的 `S(i)`, 其中 `i = 0,1,2....,n-1。`
然后我们再减去之前的` S(k)`,其中 `k = 0，1，i - 1`，中的最小值即可。 因此我们需要
用一个变量来维护这个最小值，还需要一个变量维护最大值。

#### 复杂度分析

- *时间复杂度：* `O(n) - n 是数组长度`
- *空间复杂度：* `O(1)`

Damn it!

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        maxSum = nums[0]
        minSum = sum = 0
        for i in range(n):
            sum += nums[i]
            maxSum = max(maxSum, sum - minSum)
            minSum = min(minSum, sum)
            
        return maxSum
```



#### *Result*

Runtime: 48 ms, faster than 85.21% of Python online submissions for Maximum Subarray.

Memory Usage: 12.4 MB, less than 41.02% of Python online submissions for Maximum Subarray.



Damn it he is good!