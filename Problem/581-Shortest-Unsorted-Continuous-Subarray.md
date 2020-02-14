## 581 Shortest Unsorted Continuous Subarray

### *Description*

```
Given an integer array, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the shortest such subarray and output its length.

Example 1:
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
Note:
Then length of the input array is in range [1, 10,000].
The input array may contain duplicates, so ascending order here means <=.
```





### *My Solution*

这种题目一出来我就想到用双指针，但是我写的真的是很垃圾，之前也有一道双指针题目，加了很多限制后可算是完成了，这一次完全写不下去了

Please see Trash below:

```python
class Solution(object):
    def findUnsortedSubarray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        Minpoint = 0
        Maxpoint = len(nums)-1
        Minstop = Maxstop = 0
        while Minstop==0 or Maxstop==0:
            if Minpoint >= Maxpoint and Minstop*Maxstop == 0:
                return 0
            if nums[Minpoint] > nums[Minpoint+1]:
                Minstop = 1
                for i in range(0, Minpoint+1):
                    if nums[i]>min(nums[Minpoint:Maxpoint+1]):
                        Minpoint = i
                        break;
            else:
                Minpoint += 1
            if Minstop*Maxstop == 1:
                break
            if nums[Maxpoint] < nums[Maxpoint-1]:
                Maxstop = 1
                for i in range(Maxpoint,len(nums)):
                    if nums[i] < max(nums[Minpoint:Maxpoint+1]):
                        Maxpoint = i
            else:
                Maxpoint -= 1
        return Maxpoint-Minpoint+1
```



### *Brute Force From LeetCode*

