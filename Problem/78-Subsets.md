## 78 Subsets

### *Description*

```
Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:

Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```



类似的题目需要总结一下，比如说这道题是subset，但是permutation啊 combination啊其实都差不多（from leetcode）https://leetcode.com/problems/subsets/solution/

所以这一类型的题目属于比较经典的，应该是举一反三的题目

相关题目：[22 Generate Parentheses](./Problem/22-Generate-Parentheses.md); 

下面是这三种问题的一些总结：

> First, their solution space is often quite large:
>
> - [Permutations](https://en.wikipedia.org/wiki/Permutation#k-permutations_of_n): $N!$
> - [Combinations](https://en.wikipedia.org/wiki/Combination#Number_of_k-combinations): $C_N^k = \frac{N!}{(N - k)! k!}$
> - Subsets: $2^N$, since each element could be absent or present.



一般来说有三种方法去解决这三类问题：

- Recursion
- Backtracking(这是啥？)
- Lexicographic generation based on the mapping between binary bitmasks and the corresponding permutations / combinations / subsets



### *My Solution*

题目要求的是找一个list的所有子集，可以这么看：[1,2,3]的子集是由[1,2]的子集和[3]组合而来的，首先对[1,2]求子集：[[],[1],[2],[1,2]]然后对[1,2]的所有子集屁股后面加一个[3]，再和原来的子集相加[[],[1],[2],[1,2]]+[[3],[1,3],[2,3],[1,2,3]]这样子就解决了

代码其实也很简单，但是python个坑货list只能引用不能赋值，深赋值得用copy包，所以第一次尝试用java实现：

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        result.add(new ArrayList<>());
        if(nums == null || nums.length == 0){
            return result;
        }
        int s = 0;
        for(int n:nums){
            s = result.size();
            for(int i = 0;i < s; i++){
                List<Integer> set = new ArrayList<>(result.get(i));
                set.add(n);
                result.add(set);
            }
        }
        return result;
    }
}
```



#### *Result*

Runtime: 1 ms, faster than 54.83% of Java online submissions for Subsets.

Memory Usage: 38.8 MB, less than 5.74% of Java online submissions for Subsets.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/304791813/) | 1 ms    | 38.8 MB | java     |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/304791740/) | 0 ms    | 39.1 MB | java     |



PS: Python 连new都用不了，真的辣鸡

Runtime特别好，但是memory消耗得太大了



PSS，原来Python也是可以写的，是我太垃圾了.....

```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        n = len(nums)
        output = [[]]
        
        for num in nums:
            output += [curr + [num] for curr in output]
        
        return output
```

#### *Result*

Runtime: 24 ms, faster than 45.32% of Python online submissions for Subsets.

Memory Usage: 12 MB, less than 30.51% of Python online submissions for Subsets.



### *Solution II: Lexicographic (Binary Sorted) Subsets*

一共有三种方法，recursion， backtracking，binary sorted

Recursion我自己写出来了，backtracking比较蠢不想用，binary sorted很巧妙，也是之后做combination啊permutation啊Subsets啊最好的办法

因为目标是在n个数据中找到子集，假设用一个binary list表示子集，出现的地方标1，未出现的地方标0。如此一来，问题就转换为了列出0-n的二进制数列

列出数列的代码如下：

```python
nth_bit = 1 << n
for i in range(2**n):
    # generate bitmask, from 0..00 to 1..11
    bitmask = bin(i | nth_bit)[3:]
```



然后就只需要设计一个数列与子集的映射关系即可

整体代码如下：

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        output = []
        
        nth_bit = 1 << n
        for i in range(2**n):
            # generate bitmask, from 0..00 to 1..11
            bitmask = bin(i | nth_bit)[3:]
            
            # append subset corresponding to that bitmask
            output.append([nums[j] for j in range(n) if bitmask[j] == '1'])
        
        return output
```



#### *Result*

Runtime: 20 ms, faster than 73.88% of Python online submissions for Subsets.

Memory Usage: 12 MB, less than 55.93% of Python online submissions for Subsets.