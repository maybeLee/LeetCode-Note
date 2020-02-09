## 448 Find All Numbers Disappeared in an Array

```
Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Example:

Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```



LeetCode 上有一个大佬给的方法很好，巧用set

```python
class Solution(object):
    def findDisappearedNumbers(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        return list(set(range(1,len(nums) + 1)) - set(nums))
```



#### *Result*

Runtime: 360 ms, faster than 33.88% of Python online submissions for Find All Numbers Disappeared in an Array.

Memory Usage: 20.6 MB, less than 30.77% of Python online submissions for Find All Numbers Disappeared in an Array.