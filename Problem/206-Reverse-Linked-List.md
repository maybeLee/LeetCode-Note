## 206 Reverse Linked List

```
Reverse a singly linked list.

Example:

Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?
```



看到这个题目我的第一反应是，列表的一个reverse题目：

要实现[1,2,3,4,5]列表的reverse，可以分别对列表的两个部分reverse，然后再一起reverse

``` 
    [1,2,3,4,5]
     /		\
  [1,2,3]	[4,5]
  	 |		  |
  [3,2,1]	[5,4]
  	  \		  /
  	    \	/
  	    / \
  [5,4]     [3,2,1]
```

于是想用这种方法做recursion，但是失败了，下面是官方给的答案，链表的recursion还是不太熟悉..........

### *Solution 1: Recursion*

因为是链表，你没法像list一样快速分成两段进行分别recursion，因此只能一个一个递归，假设现在递归到了第k_n 个

$1->2->3->......k_n->k_{n+1}->.......k_m$

可知$k_{n+1}->.......k_m$已经实现reverse，下面要做的是，把$k_n$放到$k_m$后面，并且在最后面加上None

具体实现方法是head.next.next = next

#### *Code*

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        #Solution 1 Recursion
        if head == None or head.next == None:
            return head
        p = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return p
```



#### *Result*

Runtime: 28 ms, faster than 39.07% of Python online submissions for Reverse Linked List.

Memory Usage: 17.5 MB, less than 5.56% of Python online submissions for Reverse Linked List.



自己对于链表的递归还是需要练习

### *Solution 2: Iteration*(BY MYSELF!!!!)

一般来说啊,.....如果递归能够用迭代代替，必然要用到队列或者栈，这道题就是用到了栈，先把所有的node（除了最后一个node）放到一个list里面，然后每次迭代把list的最后一个拿出来，用p = p.next.next 实现链表中最后两个节点之间的reverse，知道list pop 空为止

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        #Solution 2 Iteration
        if head == None or head.next == None:
            return head
        node_list = []
        while head.next != None:
            node_list.append(head)
            head = head.next
        head = node_list[-1].next
        while node_list:
            p = node_list.pop(-1)
            p.next.next = p
        p.next = None
        return head
```

**自我反省：**

这个node_list 必然浪费了一些空间，以及需要设置一个新的head标志链表的末端吗？

#### *Result*

Runtime: 28 ms, faster than 39.07% of Python online submissions for Reverse Linked List.

Memory Usage: 13.7 MB, less than 44.44% of Python online submissions for Reverse Linked List.

很棒啊！

运行时间在28ms到20ms之间，但是内存减少了将近4M



### Solution 3 from LeetCode Iteration

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        #Solution 3 Iteration ver2.0
        prev = None
        curr = head
        while curr != None:
            next_temp = curr.next
            curr.next = prev
            prev = curr
            curr = next_temp
        return prev
```



#### *Result*

Runtime: 40 ms, faster than 7.59% of Python online submissions for Reverse Linked List.

Memory Usage: 13.7 MB, less than 42.59% of Python online submissions for Reverse Linked List.



跟我自己写的差不多......