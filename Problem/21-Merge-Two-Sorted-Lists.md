## 21 Merge Two Sorted Lists

```
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```



#### *My Solution*

双链表，假设有两个链表a, b 首先创造两个指针分别指向a 和 b，判断b指向的节点能不能放在a 和 a->next 之间，如果不行的话，是看b应该放到a的左边还是a->next的右边，这样一遍一遍判断，加了很多判断条件......感觉写的很垃圾



#### *Code*

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        #Solution 1 can I use recursion?
        
        #Solution 2, Iteration
        curr1 = l1
        prev = curr2 = l2
        if l1 == None:
            return l2
        while curr1 != None and prev != None:
            if curr1.val <= curr2.val and curr1.next != None and curr1.next.val >= curr2.val:
                prev = prev.next
                curr2.next = curr1.next
                curr1.next = curr2
                curr1 = curr1.next
                curr2 = prev
            elif curr1.val>curr2.val:
                prev = prev.next
                curr2.next = curr1
                curr1 = curr2
                curr2 = prev
                l1 = curr1
            else:
                curr1 = curr1.next
        if prev != None:
            start = l1
            while start.next != None:
                start = start.next
            start.next = prev
        return l1
```



因为每次用链表都会想到能不能用递归的方法实现，但是这个代码想不出来用递归的方法去搞



ANYWAY

#### *Result*

Runtime: 24 ms, faster than 72.13% of Python online submissions for Merge Two Sorted Lists.

Memory Usage: 11.9 MB, less than 37.93% of Python online submissions for Merge Two Sorted Lists.