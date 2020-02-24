## 102 Binary Tree Level Order Traversal

### *Description*

```
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
```

树的层次遍历



### *My Solution*

就........很简单吧........这种基本的树的遍历，一个是recursion 一个是 用queue的iteration

先写一个用queue的iteration，把所有node按照层次的顺序放在queue里面，注意一个小技巧是：在不同层之间用None来隔开，这样也方便在while里面做判断

PS：最后写代码的时候，跳出循环那里伤了一下脑筋，此外还有特殊情况没有考虑好

#### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        #Solution I: stack and iteration
        if root == None:
            return []
        stack = [None, root]
        result = []
        while stack:
            node = stack.pop(0)
            if node == None:
                if stack == []: break
                result.append([])
                stack.append(None)
                continue
            result[-1].append(node.val)
            if node.left: stack.append(node.left)
            if node.right: stack.append(node.right)
        return result
```



#### *Result*

Runtime: 20 ms, faster than 81.67% of Python online submissions for Binary Tree Level Order Traversal.

Memory Usage: 12.3 MB, less than 63.23% of Python online submissions for Binary Tree Level Order Traversal.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/306050501/) | 20 ms   | 12.3 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/306050480/) | 24 ms   | 12.3 MB | python   |
| 4 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/306049643/) | 24 ms   | 12.2 MB | python   |
| 4 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/306049604/) | 24 ms   | 12.3 MB | python   |

PS: 这道题感觉用recursion做很奇怪，毕竟recursion主要侧重于深度的遍历，这种层次的遍历需要写很丑的代码



