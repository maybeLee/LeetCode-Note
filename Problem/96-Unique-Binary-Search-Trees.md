## 96 Unique Binary Search Trees

### *Description*

```
Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?

Example:

Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

这里包含了二叉树的概念？小的放左边，大的放右边



### *My Solution*

因为是combination的问题，自然而然可以用DP

用count = 0算存在的BTS个数，判断结束条件就是1....n能够完全放完。

这个问题深思一下就是爬梯子问题，click[70 Climbing Stairs](../Problem/70-Climbing-Stairs.md)

不要用recursion，这个方法太傻逼了，明显有很多重复的运算，这个地方计算有多少path唯一的变量就是有多少个数，因此可以从只有一个数开始记录路径数量，见下面

#### *Code*

```python
class Solution(object):
    def numTrees(self, n):
        """
        :type n: int
        :rtype: int
        """
        hashmap = {1:1, 2:2}
        for i in range(3, n+1):
            count = 0
            for j in range(1, i+1):
                if j == 1 or j == i:
                    count += hashmap[i-1]
                    continue
                count += hashmap[j-1]*hashmap[i-j]
            hashmap[i] = count
        return hashmap[n]
```



#### *Result*

Runtime: 12 ms, faster than 89.85% of Python online submissions for Unique Binary Search Trees.

Memory Usage: 11.8 MB, less than 27.27% of Python online submissions for Unique Binary Search Trees.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307589256/) | 12 ms   | 11.8 MB | python   |
| 3 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/307588262/) | 12 ms   | 11.8 MB | python   |

时间很好，内存比较拉瓜，把dict换成list还是一样的，说明加了一个key的内存几乎没影响