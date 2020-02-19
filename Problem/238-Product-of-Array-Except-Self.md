## 238 Product of Array Except Self

```
Given an array nums of n integers where n > 1,  return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Example:

Input:  [1,2,3,4]
Output: [24,12,8,6]
Note: Please solve it without division and in O(n).

Follow up:
Could you solve it with constant space complexity? (The output array does not count as extra space for the purpose of space complexity analysis.)
```



终 极 暴 力 解 法

### *My Solution I Brute Force*

一个list，循环第一层，找except的元素，第二层算积

```python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        Brute Force
        numlist = []
        for i in range(len(nums)):
            node = nums.pop(i)
            temp = 1
            for j in nums:
                temp *= j
            numlist.append(temp)
            nums.insert(i, node)
        return numlist
```



#### *Result*

TLE



### *My Solution II Recursion*

list [1,2,3,4,5]

第一个就是[2,3,4,5]的积，后面的就是1(list[0])和[2,3,4,5]recursion的乘积的结果

```python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if len(nums) == 2:
            return [nums[1],nums[0]]
        prod = 1
        for i in nums[1:]:
            prod *= i
        return [prod]+[x*nums[0] for x in self.productExceptSelf(nums[1:])]
```



#### *Result*

Memory Limit Exceeded

这个题目真是刁钻啊.......

### *My Solution III with extra space*

再创建一个全为1的list，对nums每一个元素进行遍历，遍历的时候对list除了该元素对应位置的元素以外其他全部乘以nums[i]

自认为这个方法还不错，结果还是TLE，因为不管怎么样做乘法的时候每一次都需要花费一个循环，后来我懒得搞了，直接用numpy 的array点乘

```python
import numpy as np
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        #I can use iteration to replace recursion
        newlist = np.array([1]*len(nums))
        for i in range(len(nums)):
            node = newlist[i]
            newlist = nums[i]*newlist
            newlist[i] = node
        return list(newlist)
            
```



#### *Result*

Runtime: 1580 ms, faster than 5.18% of Python online submissions for Product of Array Except Self.

Memory Usage: 28.1 MB, less than 7.14% of Python online submissions for Product of Array Except Self.



这道题目真的是欺人太甚

