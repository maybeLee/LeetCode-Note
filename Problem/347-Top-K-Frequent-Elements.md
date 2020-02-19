## 347 Top K Frequent Elements

### *Description*

```
Given a non-empty array of integers, return the k most frequent elements.

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
Example 2:

Input: nums = [1], k = 1
Output: [1]
Note:

You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
```



### *My Solution*

这道题一开始就会想到用hashmap先统计每一个元素出现的频率，然后就是从这些频数中找到最大的k个，想法很简单，但是找到最大的k个的时候，发现怎么样也不能达到`< O(n log n)`的条件

#### *Code*

```python
class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        #One easy solution is to use hashmap.....
        #This way can achieve less than O(nlogn) complexity
        if nums == []:
            return []
        hashmap = {}
        for i in nums:
            if i not in hashmap:
                hashmap[i] = 1
            else:
                hashmap[i] += 1
        kmap = []
        for i in range(k):
            tempMax = max(hashmap, key=lambda x: hashmap[x])
            kmap.append(tempMax)
            hashmap.pop(tempMax)
        return kmap
```



这个code里面也稍微会了一点点lambda的用法，比如说上面代码里面的`max(hashmap, key=lambda x: hashmap[x])`这个的意思就是，返回的结果是x，比较的依据是hashmap[x]，这样就成功的只比较字典的value，然后返回字典的key



#### *Result*

Runtime: 312 ms, faster than 5.03% of Python online submissions for Top K Frequent Elements.

Memory Usage: 15.1 MB, less than 100.00% of Python online submissions for Top K Frequent Elements.



| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/304144610/) | 312 ms  | 15.1 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/304144585/) | 316 ms  | 15 MB   | python   |



Runtime 太可怕了........果然这个就是brute force，但是memory用的很好，这就说明，我需要再多用一点内存来让runtime加快



### *Solution II*

现在的关键是如何用O(n)的时间复杂度实现在list中找k个最大的



答案用了Heap？？？

```python
class Solution:
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """ 
        count = collections.Counter(nums)   
        return heapq.nlargest(k, count.keys(), key=count.get) 
```



Runtime: 96 ms, faster than 55.14% of Python online submissions for Top K Frequent Elements.

Memory Usage: 15.4 MB, less than 21.95% of Python online submissions for Top K Frequent Elements.



| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/304147829/) | 96 ms   | 15.4 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/304147768/) | 96 ms   | 15.3 MB | python   |
| 9 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/304146642/) | 100 ms  | 15.3 MB | python   |



没怎么看懂