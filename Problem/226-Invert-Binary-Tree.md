## 226 Invert Binary Tree

```
Invert a binary tree.

Example:

Input:

     4
   /   \
  2     7
 / \   / \
1   3 6   9
Output:

     4
   /   \
  7     2
 / \   / \
9   6 3   1
```



> Trivia:
> This problem was inspired by this original tweet by Max Howell:
>
> Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so f*** off.

### *My Solution*

很简单recursion啦

要注意的是，左节点，右节点交换的时候需要一个临时变量（内存又浪费了......）

#### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        #Solution, Recursion
        if root == None:
            return None
        temp = Solution.invertTree(self, root.right)
        root.right = Solution.invertTree(self, root.left)
        root.left = temp
        return root
```



#### *Result*

> Runtime: 12 ms, faster than 93.65% of Python online submissions for Invert Binary Tree.
>
> Memory Usage: 11.8 MB, less than 40.00% of Python online submissions for Invert Binary Tree.

Relatively good....Okay 也可能很差，it depends.....

一般来说.....能用递归就能用迭代，可能迭代方法更好？用队列还是栈?

### *Other Solution*

用队列实现iteration

首先push进去root，然后pop root，将root的左右节点交换，再将root的左右子节点push进队列

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        #Solution, Iteration
        if root == None:
            return None
        queue = [root]
        while queue:
            node = queue.pop(0)
            node.left, node.right = node.right, node.left
            if node.left != None: queue.append(node.left)
            if node.right != None: queue.append(node.right)
        return root
```

#### *Result*

Runtime: 20 ms, faster than 47.73% of Python online submissions for Invert Binary Tree.

Memory Usage: 11.9 MB, less than 12.50% of Python online submissions for Invert Binary Tree.



That's the same......

How can I achieve more?