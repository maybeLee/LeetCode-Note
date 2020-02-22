## 287 Find the Duplicate Number

### *Description*

```
Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

Example 1:

Input: [1,3,4,2,2]
Output: 2
Example 2:

Input: [3,1,3,4,2]
Output: 3
Note:

You must not modify the array (assume the array is read only).
You must use only constant, O(1) extra space.
Your runtime complexity should be less than O(n2).
There is only one duplicate number in the array, but it could be repeated more than once.
```



兄弟题目：[136 Single Number](../Problem/136-Single-Number.md)

136是通过位运算来找到唯一一个single的，所以一开始看到这一道题也会想着用位运算，后来发现能有更简单的方法

### *My Solution I*

这道题的trick在于，我们知道所以int 的范围都是`(1,n)`所以对nums求set，如果set的长度为n+1代表没有重复的，set长度为n代表有两个重复的数，set为n-1代表有三个重复的数blablabla

得到了重复的个数之后，通过sum(nums) - sum(set(nums))的方法可以得到多出来的数的和，从而求出重复的数字

```python
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #Solution I
        return (sum(nums) - sum(set(nums)))/(len(nums) - len(set(nums)))
```



#### *Result*

Runtime: 48 ms, faster than 90.42% of Python online submissions for Find the Duplicate Number.

Memory Usage: 14.5 MB, less than 7.14% of Python online submissions for Find the Duplicate Number.



| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305694934/) | 48 ms   | 14.5 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305694886/) | 40 ms   | 14.5 MB | python   |

运算时间很给力，但是内存占用的稍微有点多？

准确的说，我的space 应该是O(n)而不是O(1)所以这种方法不行？

### *My Solution II*

两次循环.......

```python
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #Solution II
        for i in range(len(nums)):
            for j in nums[:i]:
                if nums[i] == j:
                    return j
```



#### *Result*

Runtime: 8416 ms, faster than 5.27% of Python online submissions for Find the Duplicate Number.

Memory Usage: 13.5 MB, less than 66.67% of Python online submissions for Find the Duplicate Number.



### *My Solution III*

先把nums sort一下，然后比较相邻的两个数

```python
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #Solution III
        nums.sort()
        for i in range(len(nums)-1):
            if nums[i] == nums[i+1]:
                return nums[i]
```



#### *Result*

Runtime: 48 ms, faster than 90.42% of Python online submissions for Find the Duplicate Number.

Memory Usage: 13.6 MB, less than 57.14% of Python online submissions for Find the Duplicate Number.



Memory 啊.......这种情况还是把nums改变了.......

### *LeetCode Approach: Floyd's Tortoise and Hare (Cycle Detection)*

This approach is crazy