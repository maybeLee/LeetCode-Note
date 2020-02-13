## 141 Linked List Cycle

### *Description*

```
Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

 

Example 1:

Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.


Example 2:

Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.


Example 3:

Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.

Follow up:

Can you solve it using O(1) (i.e. constant) memory?
```



### *My Solution I*

最简单的方法就是用hashmap

但这个违背了常数级memory的要求，anyway

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        #The first thought about this problem is to use hashmap to store node visited, but that costs extra memory
        hashmap = {}
        curr = head
        while curr:
            if curr in hashmap:
                return True
            else:
                hashmap[curr] = 1
            curr = curr.next
        return False
```



#### *Result*

Runtime: 44 ms, faster than 40.98% of Python online submissions for Linked List Cycle.

Memory Usage: 19.2 MB, less than 6.38% of Python online submissions for Linked List Cycle.

Oh memory....

### *LeetCode Solution*

这个太牛逼了

龟兔赛跑, 只要跑道是⚪的,跑的快的就一定会追上跑的慢的

设置两个指针,快指针一次跑两个,慢指针一次跑一个,如果快的追上慢的了,那么就代表有⚪

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        #Solution II from leetcode
        if head == None:
            return False
        slow = head
        fast = head.next
        while fast != None and fast.next != None:
            fast = fast.next.next
            slow = slow.next
            if fast == slow or fast == slow.next:
                return True
        return False
```


#### *Result*

Runtime: 40 ms, faster than 64.59% of Python online submissions for Linked List Cycle.

Memory Usage: 18.3 MB, less than 32.62% of Python online submissions for Linked List Cycle.



I like this problem