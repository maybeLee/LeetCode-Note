## 169 Majority Element

```
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

Example 1:

Input: [3,2,3]
Output: 3
Example 2:

Input: [2,2,1,1,1,2,2]
Output: 2
```



### *My Solution*

这种题目最简单的方法就是HashTable了吧......思路比较简单，直接上code



#### *Code*

```python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #The most easy-to-think method: HashTable
        HashTable = {}
        for i in nums:
            if i not in HashTable:
                HashTable[i] = 1
            else:
                HashTable[i] += 1
        for i in nums:
            if HashTable[i] > len(nums)/2:
                return i
```



#### *Result*

Runtime: 156 ms, faster than 60.01% of Python online submissions for Majority Element.

Memory Usage: 13.4 MB, less than 60.98% of Python online submissions for Majority Element.



结果这么好......我感觉我高估了LeetCode......特别是memory方面怎么能这么好呢.....



### *My Solution II 火拼法（不是）*

这个方法是之前在Lucifer上面看到的，大概就是，list中有两个不同的element，就把这两个抵消，因为list是基数，所以最后一定会存在一个数，这个数就是最终的结果

这个代码我还不太会写......到时候看lucifer的代码好了

```python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #Solution 2: 火拼法（不是）
        count, majority = 1, nums[0]
        for num in nums[1:]:
            if count == 0:
                majority = num
            if num == majority:
                count += 1
            else:
                count -= 1
        return majority
```



#### *Result*

Runtime: 212 ms, faster than 8.47% of Python online submissions for Majority Element.

Memory Usage: 13.4 MB, less than 63.41% of Python online submissions for Majority Element.

看不懂了看不懂了......明明内存应该会比Solution I 要低很多啊......

### *My Solution III Sort*

因为一共有len(nums) 个数，majority 是大于len(nums)/2 的，那么如果我先对nums 进行一个排序，必然majority是 中间那个数，下面的问题就是sort list 的问题了

```python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
		#Solution 3: Sorted bubble sort
        nums.sort()
        return nums[len(nums)/2]
```



#### *Result*

Runtime: 132 ms, faster than 99.96% of Python online submissions for Majority Element.

Memory Usage: 13.2 MB, less than 92.68% of Python online submissions for Majority Element.



### *LeetCode's Solution IV: Randomization*

随机找一个index，然后check 是不是 majority 如果是就返回，如果不是就不返回

```
import random
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #Solution 4: Randomized
        while True:
            element = random.choice(nums)
            if sum(1 for i in nums if i == element) > len(nums)/2:
                return element
```



#### *Result*

Runtime: 152 ms, faster than 73.01% of Python online submissions for Majority Element.

Memory Usage: 13.4 MB, less than 39.02% of Python online submissions for Majority Element.

我不是很喜欢这个方法......感觉不太可靠