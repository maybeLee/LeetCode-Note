## 39 Combination Sum

### *Description*

```
Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

Note:

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
Example 1:

Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
Example 2:

Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

### *My Solution*

#### Backtrack方法回顾

这道题目一开始的思路跟Subsets那道题目有点相似，都是想到了一个recursion的方法

实际上不仅仅是recursion，而应该说是BackTrack（回溯）.关于BackTrack的学习请戳链接[BackTrack](../Summary/BackTrack.md)

既然首先判断这道题的backtrack应该返回什么？

作为一个思维回顾，backtrack的递归函数返回的类型可以有三种

第一种，返回值是true/false。

```python
boolean solve(Node n) {
    if n is a leaf node {
        if the leaf is a goal node, return true
        else return false
    } else {
        for each child c of n {
            if solve(c) succeeds, return true
        }
        return false
    }
}
```

第二种，求个数，设全局counter，返回值是void；求所有解信息，设result，返回值void。

```python
void solve(Node n) {
    if n is a leaf node {
        if the leaf is a goal node, count++, return;
        else return
    } else {
        for each child c of n {
            solve(c)
        }
    }
}
```

第三种，设个全局变量best，返回值是void。

```python
void solve(Node n) {
    if n is a leaf node {
        if the leaf is a goal node, update best result, return;
        else return
    } else {
        for each child c of n {
            solve(c)
        }
    }
}
```

因为这个任务是要找到所有可能的解，并变为[[]]的形式返回，第一种单纯地判断，第二种是算有多少个解，第三种才是存解，因此用第三种。



BackTrack最重要的是，要pop

在写代码的时候，其实只需要考虑三点：

1. 路径是什么
2. 每一次迭代有多少种可以走的路径
3. 什么时候停止（结束）

核心框架

> ```python
> result = []
> def backtrack(路径, 选择列表):
>     if 满足结束条件:
>         result.add(路径)
>         return
> 
>     for 选择 in 选择列表:
>         做选择
>         backtrack(路径, 选择列表)
>         撤销选择
> ```



#### 如何在该题用backtrack

这道题麻烦的一点是，list里面的元素可以用很多次，对于list[2,3,6,7]，首先把2放进track里面，然后下一步选择就是[2,3,6,7]里面，target变为target-2，从而进行recursion

```python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        def backtrack(root, curr, target, track=[]):
            if target == root:
                curr.append(track)
                return True
            elif target < root:
                return False
            else:
                for i in candidates:
                    backtrack(i, curr, target-root, track+[i])
        curr = []
        for i in candidates:
            track = [i]
            backtrack(i, curr, target, track)
        return curr
```

但是上面代码有一个问题就是，它会把重复的路径加进去，比如说对于target=7，我track第一个node是2的话，可以得到[2,2,3]这个路径，也可以得到[2,3,2]这个路径，因此会重复很多

具体结果如下:

```
Wrong Answer
Runtime: 32 ms
Your input
[2,3,6,7]
7
Output
[[2,2,3],[2,3,2],[3,2,2],[7]]
Expected
[[2,2,3],[7]]
```

可以看到Output 中的[2,2,3], [2,3,2], [3,2,2]这三个是重复的，只保留一个就好

为了解决上述问题，应该有两个入手点：

- 方法1：在backtrack的过程中就加以限制，不让结果出现这种情况，但是暂时还没有一个比较清晰的思路

- 方法2：在backtrack计算完了之后，对结果curr的全部内容进行一个sort，然后去掉sort相同的

方法2尝试后的代码：

```python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        def backtrack(root, curr, target, track=[]):
            if target == root:
                curr.append(track)
                return True
            elif target < root:
                return False
            else:
                for i in candidates:
                    backtrack(i, curr, target-root, track+[i])
        curr = []
        sort = []
        for i in candidates:
            track = [i]
            backtrack(i, curr, target, track)
        for i in curr:
            if sorted(i) not in sort:
                sort.append(sorted(i))
        return sort
```

#### *Result*

Runtime: 712 ms, faster than 5.08% of Python online submissions for Combination Sum.

Memory Usage: 13.4 MB, less than 6.12% of Python online submissions for Combination Sum.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305348613/) | 712 ms  | 13.4 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305348572/) | 708 ms  | 13.3 MB | python   |

结果太差了......应该是方法二占用了比较多的内存和时间，毕竟sort会比较慢，backtrack设计的还是比较合理的



还需要尝试方法1，在backtrack的过程中就防止该问题的出现。

### *My Solution with BackTrack Try II*

Okay我看懂如何在backtrack里面取消重复了，比如我首先把2放进track里面recursion，那后面的3做recursion时下一次选择时就不要选2了，再下面6放进去做recursion的时候就不要考虑2和3了

```python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        def backtrack(root, totallist, target, track=[]):
            if target == root:
                curr.append(track)
                return True
            elif target < root:
                return False
            else:
                for i in range(len(totallist)):
                    backtrack(totallist[i], totallist[i:], target-root, track+[totallist[i]])
        curr = []
        for i in range(len(candidates)):
            track = [candidates[i]]
            backtrack(candidates[i], candidates[i:], target, track)
        return curr
```



#### *Result*

Runtime: 84 ms, faster than 52.38% of Python online submissions for Combination Sum.

Memory Usage: 11.9 MB, less than 36.74% of Python online submissions for Combination Sum.

| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305378862/) | 84 ms | 11.9 MB | python |
| ----------------- | ------------------------------------------------------------ | ----- | ------- | ------ |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305378785/) | 84 ms | 12 MB   | python |
| 2 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/305378211/) | 92 ms | 12 MB   | python |

可以看到runtime好很多，但是memory还是占了很多，考虑到用的是recursion，内存这么多也合理