## 283 Move Zeroes

```
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
Note:

You must do this in-place without making a copy of the array.
Minimize the total number of operations.
```

首先，这必然不能用recursion，那么思考用iteration的方法
暴力拆解法：把所有非0的数放到一个新的list里面，再数剩下有多少个0，全部加上去

This is really easy and I indeed don't want to write code right now....

```python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        #Anyway, I have to write this brutal method
        lastNonZeroFoundAt = 0
        for i in nums:
            if i != 0:
                nums[lastNonZeroFoundAt] = i
                lastNonZeroFoundAt += 1
        for i in range(lastNonZeroFoundAt, len(nums)):
            nums[i] = 0
```



#### *Result*

Runtime: 36 ms, faster than 73.55% of Python online submissions for Move Zeroes.

Memory Usage: 13 MB, less than 5.06% of Python online submissions for Move Zeroes.



Anyway, Python is Bullshit

