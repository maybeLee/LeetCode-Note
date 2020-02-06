## Question 617 Merge Two Binary Trees:

```
Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of new tree.

**Example 1:**


Input: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
Output: 
Merged tree:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7


**Note:** The merging process must start from the root nodes of both trees.
```

####  *Solution* By myself:

因为是二叉树，所以很自然想到用递归的方法，每个节点都判断一下能不能merge，要是能merge就两个值加起来，要是不能merge就返回两个节点中不为空的节点

*需要注意的是：*自己一开始写的时候为了方便，直接又开辟了一个新的空间存放二叉树，后来发现完全不需要，可以在之前的其中一个节点上面进行操作

**Code:**

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def mergeTrees(self, t1, t2):
        """
        :type t1: TreeNode
        :type t2: TreeNode
        :rtype: TreeNode
        """
        if t1 != None and t2 != None:
            t1.val = t1.val+t2.val
            t1.left = Solution.mergeTrees(self, t1.left, t2.left)
            t1.right = Solution. mergeTrees(self, t1.right, t2.right)
        elif t1 == None:
            return t2
        elif t2 == None:
            return t1
        return t1
```

**Result**

Runtime: 76 ms, faster than 65.63% of Python online submissions for Merge Two Binary Trees.

Memory Usage: 13.2 MB, less than 16.67% of Python online submissions for Merge Two Binary Trees.

#### Other solutions

LeetCode上面介绍了一种通过栈的方式进行iteration的操作，比递归难一些，具体方法如下：

每一次都会往栈里面放入一个node pair，分别是两个树的对应node，如果这两个node都是None，代表这两个对应节点没有，如果两个node都不是None，则表示存在相对应

比较抽象......https://leetcode.com/articles/merge-two-binary-trees/ 这个文章中有一个ppt视频，根据这个ppt就比较容易理解了......

**Code:**

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def mergeTrees(self, t1, t2):
        """
        :type t1: TreeNode
        :type t2: TreeNode
        :rtype: TreeNode
        """
		#Solution 2 iteration
        if t1 == None:
            return t2;
        stack = [[t1, t2]]
        while(stack != []):
            pop_list = stack.pop()
            if pop_list[1] == None:
                continue
            pop_list[0].val += pop_list[1].val
            if pop_list[0].left == None:
                pop_list[0].left = pop_list[1].left
            else:
                stack.append([pop_list[0].left, pop_list[1].left])
            if pop_list[0].right == None:
                pop_list[0].right = pop_list[1].right;
            else:
                stack.append([pop_list[0].right, pop_list[1].right])
            
        return t1
```



**Result**(时间会有变动，主要是内存方面会少一些)

Runtime: 76 ms, faster than 65.63% of Python online submissions for Merge Two Binary Trees.

Memory Usage: 12.8 MB, less than 47.22% of Python online submissions for Merge Two Binary Trees.



***通过这个stack啊.....我发现python的 “=”是存在引用性质的？像字典啊，class啊这些变量相等的时候是会共用存储空间的，这还是蛮方便的。***