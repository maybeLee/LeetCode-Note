## 215 Kth Largest Element in an Array

### *Description*

```
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Example 1:

Input: [3,2,1,5,6,4] and k = 2
Output: 5
Example 2:

Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.
```



### *My Solution I*

一种很简单的方法就是逐次pop掉最大的

#### *Code*

```python
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        while k != 0:
            node = nums.pop(nums.index(max(nums)))
            k -= 1
        return node
```



#### *Result*

Runtime: 596 ms, faster than 21.91% of Python online submissions for Kth Largest Element in an Array.

Memory Usage: 12.3 MB, less than 69.81% of Python online submissions for Kth Largest Element in an Array.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305718506/) | 596 ms  | 12.3 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305718492/) | 596 ms  | 12.2 MB | python   |
| 2 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/305718287/) | 592 ms  | 12.4 MB | python   |

max 和 index 函数耗时还是比较大的

### *My Solution II*

