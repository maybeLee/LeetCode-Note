## 101 Symmetric Tree

### *Description*

```
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3
 

But the following [1,2,2,null,3,null,3] is not:

    1
   / \
  2   2
   \   \
   3    3
 

Note:
Bonus points if you could solve it both recursively and iteratively.
```



WOW I made it!!!



### *My Solution*

Okay, what I am saying is to use two queue to store the left tree and the right tree orderly, I will pop one of each stack in every iteration and compare their value, if that is not equal then return false, until the stack is empty



Anyway I add many if condition, which makes the code quite ugly

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        #Iteration Way
        if root == None:
            return True
        stack_l = [root.left]
        stack_r = [root.right]
        while stack_l and stack_r:
            node_l = stack_l.pop(0)
            node_r = stack_r.pop(0)
            if node_l == None and node_r == None:
                break
            elif node_l == None or node_r == None:
                return False
            if node_l.val != node_r.val:
                # print(node_l, node_r)
                return False
            else:
                if node_l.left and node_r.right: 
                    stack_l.append(node_l.left)
                    stack_r.append(node_r.right)
                elif node_l.left or node_r.right:
                    return False
                if node_l.right and node_r.left:
                    stack_l.append(node_l.right)
                    stack_r.append(node_r.left)
                elif node_l.right or node_r.left:
                    return False
        return True
```



I made some simplification

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        #Recursion Way
        if root == None:
            return True
        stack_l = [root.left]
        stack_r = [root.right]
        while stack_l and stack_r:
            node_l = stack_l.pop(0)
            node_r = stack_r.pop(0)
            if node_l == None and node_r == None:
                continue
            elif node_l == None or node_r == None:
                return False
            if node_l.val != node_r.val:
                # print(node_l, node_r)
                return False
            else:
                stack_l.append(node_l.left)
                stack_r.append(node_r.right)
                stack_l.append(node_l.right)
                stack_r.append(node_r.left)
        return True
```



It seems like I am always intend to add duplicate if condition



### *Result*

Runtime: 24 ms, faster than 48.70% of Python online submissions for Symmetric Tree.

Memory Usage: 12 MB, less than 41.30% of Python online submissions for Symmetric Tree.

https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)

Show off your acceptance:

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/302359140/) | 24 ms   | 12 MB   | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/302359121/) | 28 ms   | 12.1 MB | python   |
| a minute ago      | [Accepted](https://leetcode.com/submissions/detail/302358944/) | 28 ms   | 12 MB   | python   |
| a minute ago      | [Accepted](https://leetcode.com/submissions/detail/302358896/) | 20 ms   | 12.2 MB | python   |
| 2 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/302358850/) | 28 ms   | 12.1 MB | python   |

Actually not that good, but still okay

