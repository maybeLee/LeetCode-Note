## 543 Diameter of Binary Tree

***Description***

```
Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

Example:
Given a binary tree
          1
         / \
        2   3
       / \     
      4   5    
Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

Note: The length of path between two nodes is represented by the number of edges between them.
```



### *My Solution*

一样，二叉树看着就recursion

因为最大宽度一共有三种情况，经过root （左分支深度+右分支深度），左分支最大宽度，右分支最大宽度

因此需要做的就是，每一次recursion都算一下经过root的宽度，然后比较和左分支最大宽度以及右分支最大宽度进行比较

因此，问题变为如何求一个树的最大深度，这个在之前的题目中做到过，用BFS的层次遍历方法，为了方便看，我把计算深度单独写成了一个函数



#### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root == None:
            return 0
        leftDepth = self.maxDepth(root.left)
        rightDepth = self.maxDepth(root.right)
        return max(self.diameterOfBinaryTree(root.left), self.diameterOfBinaryTree(root.right), leftDepth+rightDepth)
        
    def maxDepth(self, root):#This function is used for depth calculation
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

#### *Result*

Runtime: 852 ms, faster than 5.26% of Python online submissions for Diameter of Binary Tree.

Memory Usage: 14.5 MB, less than 92.31% of Python online submissions for Diameter of Binary Tree.



emmm毕竟递归里面还用了循环，队列，时间确实消耗太大，但是memory占用情况还不错啊



LeetCode上面的答案是错的吧？