## 104. Maximum Depth of Binary Tree

```
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

Example:

Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
return its depth = 3.
```

### *Solution By myself*

因为是二叉树，所以万能递归lol........

一个节点有两条路，根据动态规划的算法，必然是往深度最深的路走，按照这个方法进行递归

##### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        #Solution 1 Brutal Recursion
        if root == None:
            return 0
        return 1+max(Solution.maxDepth(self, root.left), Solution.maxDepth(self, root.right))
```

##### *Result*

Runtime: 36 ms, faster than 26.54% of Python online submissions for Maximum Depth of Binary Tree.

Memory Usage: 16.1 MB, less than 6.17% of Python online submissions for Maximum Depth of Binary Tree.

必然的lol，这个递归浪费了很多节点存储空间和遍历，并没有了解到深度等等的特性



### *Other Solution*

思考：可以尝试动态规划或者贪婪算法进行？

然并卵，Lucifer 汇总了一个用队列实现iteration的方法，运用的是二叉树的层次遍历BFS

什么是层次遍历？如何实现层次遍历？请戳[直通车](#BFS)

下面只要实现层次遍历就好，遍历了多少层就代表有多少深度



##### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        #Solution 2 Iteration with queue
        if root == None:
            return 0
        queue, depth = [root, None], 1
        while queue:
            node = queue.pop(0)
            if node:
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)
            elif queue:
                queue.append(None)
                depth += 1
        return depth
```



##### *Result*

Runtime: 32 ms, faster than 56.01% of Python online submissions for Maximum Depth of Binary Tree.

Memory Usage: 14.7 MB, less than 27.16% of Python online submissions for Maximum Depth of Binary Tree.



slightly better.......







### *BFS*

层次遍历的关键点在于如何记录每一层次是否遍历完成， 我们可以用一个标识位来表式当前层的结束。

![binary-tree-traversal-bfs](D:/Study/LeetCode/leetcode/assets/thinkings/binary-tree-traversal-bfs.gif)

(图片来自 https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/tree/breadth-first-search)

具体做法：

1. 根节点入队列， 并入队列一个特殊的标识位，此处是 null

2. 出队列

3. 判断是不是 null， 如果是则代表本层已经结束。我们再次判断是否当前队列为空，如果不为空继续入队一个 null，否则说明遍历已经完成，我们什么都不不用做

4. 如果不为 null，说明这一层还没完，则将其左右子树依次入队列。

