## 160 Intersection of Two Linked Lists

### *Description*

```
Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:


begin to intersect at node c1.

 

Example 1:


Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
Output: Reference of the node with value = 8
Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
 

Example 2:


Input: intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
Output: Reference of the node with value = 2
Input Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [0,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
 

Example 3:


Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: null
Input Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
 

Notes:

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.
```



### *My Solution*

哈希表，先遍历一边A，把A的节点存起来，然后再遍历B，如果B的节点有在A中出现的，就返回那个节点，如果B遍历完了都没有出现，就返回None



我的想法是因为字典又要存key 又要存value，我又只需要记录节点是否存在，value就没有用了，那不如用列表，这样更省内存？结果用列表跑就会出现TLE，然是换做用字典做存储就不会出现这个情况？？？WTF！！！

用列表跑的code：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        #Another Hashmap
        hashmap = []
        if headA == None or headB == None:
            return None
        while headA:
            hashmap.append(headA)
            headA = headA.next
        while headB:
            if headB in hashmap:
                return headB
            headB = headB.next
        return None
```



#### *Result*

TLE



用字典跑的code：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        #Another Hashmap
        hashmap = {}
        if headA == None or headB == None:
            return None
        while headA:
            hashmap[headA] = headA.next
            headA = headA.next
        while headB:
            if headB in hashmap:
                return headB
            headB = headB.next
        return None
```



#### *Result*

Runtime: 200 ms, faster than 55.39% of Python online submissions for Intersection of Two Linked Lists.

Memory Usage: 42.5 MB, less than 5.33% of Python online submissions for Intersection of Two Linked Lists.



为啥用字典就可以用列表就不行？

我怀疑啊，主要在判断节点是否在字典/列表上面这一个地方出了问题。

列表是顺序结构，所以判断的时候可能要从上往下一直找，字典是无序的引用存储，判断节点是否在字典中的时候会更加容易？

这一想法还需要被证实



题外话，还写了一个只用一个while去搞的，但是跑出来内存时间差不多，就无所谓了，代码如下：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        I love hashmap
        hashmap = {}
        currA = headA
        currB = headB
        while currA or currB:
            if currA in hashmap:
                return currA
            elif currA:
                hashmap[currA] = currA.next
            if currB in hashmap:
                return currB
            elif currB:
                hashmap[currB] = currB.next
            if currA: currA = currA.next
            if currB: currB = currB.next
        return None
```


