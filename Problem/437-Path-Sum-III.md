## 437 Path Sum III

### *Description*

```
You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

Example:

root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```



### *My Solution: Recursion*

One quite stupid way is to use recursion

first root, if root != sum, then the path might be [root, root.left, ...] or [root.left, ......] the right direction is the same



#### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def pathSum(self, root, sum):

        if not root:
            return 0
        
        self.ans = 0

        def search(root, memo):
            
            self.ans += memo.count(sum)
            
            if root.left:
                search(root.left, [x+root.left.val for x in memo] + [root.left.val])
            
            if root.right:
                search(root.right, [x+root.right.val for x in memo] + [root.right.val])
                
        search(root, [root.val])
        return self.ans
```



#### *Result*

Runtime: 232 ms, faster than 65.13% of Python online submissions for Path Sum III.

Memory Usage: 30.6 MB, less than 9.09% of Python online submissions for Path Sum III.



Since I have used recursion, the memory is easy to be terrible.