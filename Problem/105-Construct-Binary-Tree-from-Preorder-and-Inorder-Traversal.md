## 105 Construct Binary Tree from Preorder and Inorder Traversal

### *Description*

```
Given preorder and inorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given

preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
Return the following binary tree:

    3
   / \
  9  20
    /  \
   15   7
```



给出一个二叉树的前序遍历，中序遍历，返回一个树



### *My Solution*

这道题目要根据前序遍历和中序遍历的性质来，还有的话，就是二叉树都可以用递归解决

对于前序遍历来说，第一个必然是根，从而可以根据这一个找到中序遍历的根，然后中序遍历的根的左侧就是左分支，右侧就是右分支，再根据这个找到前序遍历的左分支和右分支，然后将左分支和右分支一依次递归进行下面的操作。

现在有一个问题是，如何解决两个节点的值相同的情况？比如说：

```
		1						pre: [1, 3, 1, 7, 5, 3]
	   / \						in: [1, 3, 7, 1, 5, 3]
	  3   5
	 / \   \
    1	7   3
```

这种情况，如何根据pre的第一个找到in的根？

woc 题目里面说：

> You may assume that duplicates do not exist in the tree.

是不是就代表不需要考虑重复的了？

#### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        if preorder == []:
            return None
        root = TreeNode(preorder[0])
        rootIndex = inorder.index(preorder[0]) #locate root in inorder
        inLeft = inorder[:rootIndex]
        inRight = inorder[rootIndex+1:]
        preLeft = preorder[1:len(inLeft)+1]
        preRight = preorder[len(inLeft)+1:]
        root.left = self.buildTree(preLeft, inLeft)
        root.right = self.buildTree(preRight, inRight)
        return root
```



#### *Result*

Runtime: 204 ms, faster than 21.92% of Python online submissions for Construct Binary Tree from Preorder and Inorder Traversal.

Memory Usage: 87.1 MB, less than 6.06% of Python online submissions for Construct Binary Tree from Preorder and Inorder Traversal.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/308912814/) | 204 ms  | 87.1 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/308912729/) | 184 ms  | 87.1 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/308912699/) | 192 ms  | 87 MB   | python   |

Crap............

凭啥runtime 和 memory都爆炸? 我这个recursion应该是runtime不错 recursion比较爆炸？

runtime应该是O(nlogn)?



### *Solution From LeetCode With Stack, O(n)*

这个方法的出发点是先序遍历和中序遍历的末尾存在一个关系。

先序遍历的结尾要么是左叶子要么是右叶子

中序遍历的结尾要么是中间节点，要么是右叶子

因此如果先序和中序的最后一个是一样的，就必然是右叶子，如果倒数第二个也相同，那么必然是中间节点，如果倒数第二个不相同，那么先序的倒数第二个是左叶子，中序的倒数第二个是先序的倒数第三个：中间节点



#### *Code*

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        #Solution II stack from Leet discuss  
        n = len(inorder)
        j = n - 1
        stack = []

        for i in range(n - 1, -1, -1):
            node = TreeNode(inorder[i])
            last = None

            while stack and stack[-1].val == preorder[j]:
                last = stack.pop()
                j -= 1
            
            if last:
                node.right = last
            
            if stack:
                stack[-1].left = node
            
            stack.append(node)
        
        return stack[0] if stack else None
```



#### *Result*

Runtime: 36 ms, faster than 99.38% of Python online submissions for Construct Binary Tree from Preorder and Inorder Traversal.

Memory Usage: 15.5 MB, less than 93.94% of Python online submissions for Construct Binary Tree from Preorder and Inorder Traversal.



这个方法真的牛逼，我是想不出来的