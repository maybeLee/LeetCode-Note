## 46 Permutations

### *Description*

```
Given a collection of distinct integers, return all possible permutations.

Example:

Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```





### *My Solution: Recursion*

因为这道题目很容易想到recursion，因为length为4的列表的permute是在length为3的基础上完成的，所以每一次就把要放在最前面的元素拿出来，然后其他的元素再进行permutation，主要是这个方法要进行两层循环，看起来很蠢.......



#### *Code*

```python
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        #One easy way is to do recursion
        if len(nums) < 2:
            return [nums]
        if len(nums) == 2:
            return [[nums[0], nums[1]],[nums[1], nums[0]]]
        else:
            final = []
            for i in range(len(nums)):
                node = nums.pop(i)
                num = self.permute(nums)
                for j in range(len(num)):
                    final.append([node]+num[j])
                nums.insert(i, node)
            return final
```



#### *Result*

Runtime: 28 ms, faster than 65.94% of Python online submissions for Permutations.

Memory Usage: 12 MB, less than 16.00% of Python online submissions for Permutations.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/303757990/) | 28 ms   | 12 MB   | python   |
| 2 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/303757442/) | 32 ms   | 11.9 MB | python   |
| 2 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/303757403/) | 24 ms   | 12 MB   | python   |

Runtime 还行，但是memory占用比较大（毕竟用了递归）



有没有一种方法就是，把之前跑过的结果存起来，可能之后会再用到？



之后再说吧.....