## 136 Single Number

```
Given a non-empty array of integers, every element appears twice except for one. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

Example 1:

Input: [2,2,1]
Output: 1
Example 2:

Input: [4,1,2,1,2]
Output: 4
```



### *My Stupid Solution*

很理所应当地想到用哈希表去做这个任务，首先将array遍历一边，如果一个元素出现了两次，哈希表就为1，否则为0，然后再去遍历一遍把那个0返回

##### *Code*

```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #Stupid Solution, using HashTable
        HashTable = {}
        for i in nums:
            HashTable[i] = (i in HashTable)*1
        for i in nums:
            if HashTable[i] == 0:
                return i
```



##### *Result*

Runtime: 80 ms, faster than 36.51% of Python online submissions for Single Number.

Memory Usage: 14.3 MB, less than 8.11% of Python online submissions for Single Number.



时间上达标了，但是空间上不行



#### *Refinement of the above solution*

在LeetCode上提出了用hashtable的另一种表达方法，不是修改值，而是pop 内容，比我上面的方法好一些

```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #Stupid Solution, using HashTable
        HashTable = {}
        for i in nums:
            try:
                HashTable.pop(i)
            except:
                HashTable[i] = 1
        return HashTable.popitem()[0]
```

Anyway, 结果是一回事.............

### *Solution II*

#### Math

**Concept**

2 * (a + b + c) - (a + a + b + b + c) = c2∗(*a*+*b*+*c*)−(*a*+*a*+*b*+*b*+*c*)=*c*

```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return 2 * sum(set(nums)) - sum(nums)
```

WOW...........

### *Solution III*

位运算.....

```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        a = 0
        for i in nums:
            a ^= i
        return a
```

第二次了.....希望第三次能够记得这个方法



##### *Result*

Runtime: 68 ms, faster than 83.87% of Python online submissions for Single Number.

Memory Usage: 13.6 MB, less than 63.51% of Python online submissions for Single Number.

