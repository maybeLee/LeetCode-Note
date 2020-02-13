## 234 Palindrome Linked List

### *Description*

```
Given a singly linked list, determine if it is a palindrome.

Example 1:

Input: 1->2
Output: false
Example 2:

Input: 1->2->2->1
Output: true
Follow up:
Could you do it in O(n) time and O(1) space?
```



### *My Solution*

Use list to store the value of linked list, it is much more easy to deal with list than linked list



```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        #Solution 1 with extra memory
        curr = head
        stack = []
        while curr:
            stack.append(curr.val)
            curr = curr.next
        i = 0
        j = len(stack)-1
        while i<=j:
            if stack[i]!=stack[j]:
                return False
            i += 1
            j -= 1
        return True
```



### *Result*

Runtime: 64 ms, faster than 90.53% of Python online submissions for Palindrome Linked List.

Memory Usage: 30.9 MB, less than 48.28% of Python online submissions for Palindrome Linked List.



The memory thing impressed my, I thought we have to make the space complexity in O(1)....



### *Solution II with O(1) space complexity*

Okay I find one, which is not that smart but meet the requirement

(我才发现之前写的都是英文.........)

先把链表的后半部分找出来(一个while), 然后对后半部分reverse一下,接着比对后半部分和前半部分

#### *Code*

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """        
        #Solution 2 with space complexity
        curr = head
        length = 0
        while curr:
            curr = curr.next
            length += 1
        half = length /2
        curr = head
        while half:
            curr = curr.next
            half -= 1
        reverse = self.reverseList(curr)
        curr = head
        while reverse:
            if curr.val != reverse.val:
                return False
            curr = curr.next
            reverse = reverse.next
        return True
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



该方法中运用到了之前的[reverse linked list](./Problem/206-Reverse-Linked-List.md)问题

#### *Result*

Runtime: 60 ms, faster than 96.74% of Python online submissions for Palindrome Linked List.

Memory Usage: 30.8 MB, less than 72.41% of Python online submissions for Palindrome Linked List.



因为我也用了很多中间变量,所以感觉其实improvement不是特别大,而且解决方法很蠢.......



