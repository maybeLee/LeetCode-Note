## 94 Binary Tree Inorder Traversal

### *Description*

```
Given a binary tree, return the inorder traversal of its nodes' values.

Example:

Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
Follow up: Recursive solution is trivial, could you do it iteratively?
```



按照节点值的顺序遍历？左-中-右的方式遍历

### *My Solution: Recursion*

这道题好像Lucifer有讲过，关于树应该怎么遍历的，我之前看过但是忘了，现在尝试自己用recursion做一下

本来以为很难，后来发现真的很简答......

#### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root == None:
            return []
        return self.inorderTraversal(root.left)+[root.val]+self.inorderTraversal(root.right)
```



#### *Result*

Runtime: 16 ms, faster than 76.45% of Python online submissions for Binary Tree Inorder Traversal.

Memory Usage: 11.9 MB, less than 23.75% of Python online submissions for Binary Tree Inorder Traversal.



### *My Solution: Iteration*

众所周知，能用recursion就能用iteration，而且一般来说都是加一个queue，或者stack



#### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        #I love iteration(queue or stack?) stack
        if root == None:
            return []
        stack = [root]
        List = []
        while stack:
            node = stack.pop(-1)
            if node.left:
                stack.append(node)
                stack.append(node.left)
                node.left = None
            elif node.right:
                List.append(node.val)
                stack.append(node.right)
            else:
                List.append(node.val)
        return List
```



这个地方的stack跟别的题目的不同点在于，每pop一个元素的时候，不是一定要读它的值的，需要看左分支还有没有，要是还有的话，就得等等再读，所以while里面加了三种判断进行讨论

感觉自己对树的递归和迭代越来越熟悉了.....

#### *Result*

Runtime: 20 ms, faster than 45.57% of Python online submissions for Binary Tree Inorder Traversal.

Memory Usage: 11.8 MB, less than 31.25% of Python online submissions for Binary Tree Inorder Traversal.



相比recursion而而言，memory有进步，然是runtime不行.....