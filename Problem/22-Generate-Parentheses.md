## 22 Generate Parentheses

### *Description*

```
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```



### *My Solution*

首先还是分析一下这个问题，乍一看很可怕看不懂，多看两眼就发现窍门了，啥叫一个正确的solution呢，就是每一个`(` 都有一个`)`与它对应，所以不可能出现没有`(`就出现`)`的情况

记`(`出现的次数为n，那么`)`出现的次数一定不大于n

因此我的解决方法是，首先把`(`固定，然后在每个`(`之前插入任意数量的`)`前提是，插入的`)`数量不应该大于已有的`(`数量

比如当n=4时：

`(_(_(_(`

在`-`处插入一定数量限制的`)`，假定一共要插n个，初始化变量`Sum = n`那么第一个位置可以插入`)`的数量应该为`range(0, Sum-n+2) (0,Sum-n+1)`，第一个位置判断完并且插入了i个`)`后，`n-=1, Sum-=i`接着将n=3 和 新的Sum放入计算函数中。



这样讲太抽象了，举个例子：

第一个位置`)`可以放0个或者1个，如果放0个，第二个位置的`)`可以放0、1或者2个；如果第一个位置放了一个，那么第二个位置`)`只能放0或者1个

将`)`的排列数量方式用固定位置应该放多少个来表示，因此字符串的排列就变成了列表的排列

我感觉我的思路是好的，真正实现还是蛮麻烦的

#### *Code*

```python
class Solution(object):
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        def ListSum(n, Sum):
            tempList = []
            if n == 2:
                for i in range(Sum):
                    tempList.append([i,Sum-i])
                return tempList
            else:
                for i in range(Sum-n+2):
                    temp = ListSum(n-1, Sum-i)
                    for j in range(len(temp)):
                        tempList.append([i]+temp[j])
                return tempList
        if n == 1:
            return ["()"]
        final_list = ListSum(n, n)
        stringlist = []
        for i in final_list:
            string = ""
            for j in i:
                string += "(" + j*")"
            stringlist.append(string)
        return stringlist
```



#### *Result*

Runtime: 24 ms, faster than 54.39% of Python online submissions for Generate Parentheses.

Memory Usage: 12.2 MB, less than 5.88% of Python online submissions for Generate Parentheses.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/303772087/) | 24 ms   | 12.2 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/303772032/) | 24 ms   | 12.4 MB | python   |
| a minute ago      | [Accepted](https://leetcode.com/submissions/detail/303771878/) | 28 ms   | 12.2 MB | python   |



每个ListSum函数可能都会搞两次循环，然后循环里面还有自身递归......Memory估计就炸了