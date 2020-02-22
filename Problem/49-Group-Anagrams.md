## 49 Group Anagrams

### *Description*

```
Given an array of strings, group anagrams together.

Example:

Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
Note:

All inputs will be in lowercase.
The order of your output does not matter.
```



### *My Solution I stupid hashmap*

根据昨天的经验，如何判断“abs” 和 "bsa"是一样的？直接比较两个字符串sort之后的结果就好，但是sort毕竟很耗时，所以结果不是很好

#### *Code*

```python
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        #Solution I: stupid way
        if strs == []:
            return []
        cache = []
        result = []
        for i in strs:
            sor = sorted(i)
            if sor in cache:
                result[cache.index(sor)].append(i)
            else:
                result.append([i])
                cache.append(sor)
        return result
```



一个cache memory当作hashmap，另一个result存final 结果

#### *Result*

Runtime: 636 ms, faster than 6.66% of Python online submissions for Group Anagrams.

Memory Usage: 16.5 MB, less than 18.75% of Python online submissions for Group Anagrams.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305676907/) | 636 ms  | 16.5 MB | python   |
| 2 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/305676448/) | 648 ms  | 16.6 MB | python   |

结果不好很正常，完全没有一点算法的智慧

高级一点的写法：虽然dict不能用list作为key，但是dict能够用tuple作为key，这样hashmap会小很多，也不用什么乱七八糟的list来记录了

```python
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        #Solution I: stupid way
        result = collections.defaultdict(list)
        for i in strs:
            result[tuple(sorted(i))].append(i)
        return result.values()
```

Say Hi to collections datatype

#### *Result*

Runtime: 80 ms, faster than 93.12% of Python online submissions for Group Anagrams.

Memory Usage: 16.2 MB, less than 41.67% of Python online submissions for Group Anagrams.



### *My Solution II*

可能可以count？