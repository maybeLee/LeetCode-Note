## 114 Flatten Binary Tree to Linked List

### *Description*

```
Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:

    1
   / \
  2   5
 / \   \
3   4   6
The flattened tree should look like:

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

深度遍历？然后通过树的形式打印出来？

### *My Solution*

用栈深度遍历需要多用一个list的空间，线性的时间复杂度

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: None Do not return anything, modify root in-place instead.
        """
        if root == None:
            return []
        stack = [root]
        listNode = []
        while stack:
            node = stack.pop(-1)
            if node.right: stack.append(node.right)
            if node.left: stack.append(node.left)
            listNode.append(node)
        temp = root
        temp.left = temp.right = None
        for i in range(1, len(listNode)):
            listNode[i].left = None
            listNode[i].right = None
            temp.right = listNode[i]
            temp = listNode[i]
```

#### *Result*

Runtime: 28 ms, faster than 48.00% of Python online submissions for Flatten Binary Tree to Linked List.

Memory Usage: 12.7 MB, less than 8.00% of Python online submissions for Flatten Binary Tree to Linked List.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307914291/) | 28 ms   | 12.7 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307914179/) | 28 ms   | 12.7 MB | python   |

确实浪费了很多memory，尝试对树的内存进行优化



优化的结果

#### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: None Do not return anything, modify root in-place instead.
        """
        #Add a list
        if root == None:
            return []
        stack = [root]
        temp = None
        while stack:
            node = stack.pop(-1)
            if temp != None:
                temp.right = node
            if node.right: stack.append(node.right)
            if node.left: stack.append(node.left)
            temp = node
            temp.left = None
```

Runtime: 24 ms, faster than 78.08% of Python online submissions for Flatten Binary Tree to Linked List.

Memory Usage: 12.6 MB, less than 12.00% of Python online submissions for Flatten Binary Tree to Linked List.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307917784/) | 24 ms   | 12.6 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307917759/) | 24 ms   | 12.7 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307917732/) | 20 ms   | 12.8 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307917700/) | 28 ms   | 12.6 MB | python   |
| a minute ago      | [Accepted](https://leetcode.com/submissions/detail/307917634/) | 16 ms   | 12.5 MB | python   |

时间上快一些了，但是内存还是没变化啊......现在的问题就在于，我只用了一个树的内存，而且深度遍历也是必须的......



### *Solution from LeetCode*

也是一样的思路，最后的效果也是一样的差，但是代码很好看，可以学者写一下

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: None Do not return anything, modify root in-place instead.
        """
        def helper( node):
        
            if node:

                # DFS travesal to next level
                helper( node.right )
                helper( node.left )

                # flattern binary tree to right skewed linked list
                node.right = self.previous_traversal
                node.left = None
                self.previous_traversal = node
                
        # ---------------------
        
        # record of node of previous traversal
        self.previous_traversal = None
        helper(root)
```

