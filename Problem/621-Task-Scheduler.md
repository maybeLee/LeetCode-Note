## 621 Task Scheduler

### *Description*

```
Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks. Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.

 

Example:

Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
 

Note:

The number of tasks is in the range [1, 10000].
The integer n is in the range [0, 100].
```



大概是CPU的一个线性工作功能实现，熟悉操作系统的话应该还比较容易理解题目的意思。一共有A-Z种事件类型，相同两个事件之间需要有至少n个事件的节点（不足n个的，用idle）





### *My Solution*

#### *First Thought*

除了输入的list以外，外加一个list来存储每一个事件下一次发生需要等待多少个回合，如果某一个循环的时候发现list里面所有事件都无法发生，则idle

但是需要考虑，如果有两个事件都可以发生的话，应该选择哪一个发生？可能还是需要用BackTrack？但是用backtrack明显会浪费很多空间

对于每一种事件来说，能够影响是否选择它的因素有两个：

- 它这一回合能否被运行
- 它还剩多少个事例需要做

这么一看，应该需要两个space，一个list用来存储各种类事例还剩多少个需要y做，另一个list用来存储各种事例是否可以被运行。

其次考虑优先级问题，是否应该优先考虑剩余事例更多的事件种类？

我的回答：是的，因为这道题的最优解应该是CPU的idle时间最小的情况，毕竟工作量总是那么多，所以只有种类越多，CPU才可能越忙碌

#### *Code*

```python
class Solution(object):
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        hashmap = {}
        listTime = {} #shoule mode n+1 in each iteration
        for i in tasks:
            if i not in hashmap:
                hashmap[i] = 1
            elif i in hashmap:
                hashmap[i] += 1
            if i not in listTime:
                listTime[i] = 0
        count = 0
        while sum(hashmap.values()) != 0:
            maxNode = ""
            maxValue = 0
            for i in hashmap:
                if hashmap[i] > maxValue and listTime[i] == 0:
                    maxValue = hashmap[i]
                    maxNode = i
            for i in listTime:
                if listTime[i] != 0:
                    listTime[i] = (listTime[i]+1)%(n+1)
            if maxNode != "":
                hashmap[maxNode] -= 1
                listTime[maxNode] = (listTime[maxNode]+1)%(n+1)
            count += 1

        
        return count
```



#### *Result*

TLE.......

这也只有$O(n^2)$的复杂度啊.........

python 本来就慢，再加上字典调用比较耗时间



### *Solution From LeetCode*

```python
'''

Example explanation:

tasks = ["A","A","A","B","B","B"], n = 2

Procedure:

1.
# Build a dictionary for tasks
# key   : task
# value : occurrence of task

max_occ = 3

number_of_taks_of_max_occ = 2 with {'A', 'B'}

2.
#Make (max_occ - 1) = 2 groups, groups size = n+1 = 3
#Fill each group with uniform iterleaving as even as possible

group = '_ _ _' with size = 3

=> make 2 groups with uniform iterleaving 

A B _ A B _

3.
# At last, execute for the last time of max_occ jobs

A B _ A B _ A B


length of task scheduling with cooling = 8

'''


from collections import Counter

class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        
        if n == 0:
            # Quick response for special case on n = 0
            # no requirement for cooling, just do those jobs in original order
            return len(tasks)
        
        
        # key   : task
        # value : occurrence of tasks 
        task_occ_dict = Counter( tasks )
        
        # max occurrence among tasks
        max_occ = max( task_occ_dict.values() )
        
        # number of tasks with max occurrence
        number_of_taks_of_max_occ = sum( ( 1 for task, occ in task_occ_dict.items() if occ == max_occ ) )
        
        # Make (max_occ-1) groups, each groups size is (n+1) to meet the requirement of cooling
        # Fill each group with uniform iterleaving as even as possible
        
        # At last, execute for the last time of max_occ jobs
        intervl_for_schedule = ( max_occ-1 )*( n+1 ) + number_of_taks_of_max_occ
        
        # Minimal length is original length on best case.
        # Otherswise, it need some cooling intervals in the middle
        return max( len(tasks), intervl_for_schedule)
```



#### *Result*

Runtime: 388 ms, faster than 64.91% of Python online submissions for Task Scheduler.

Memory Usage: 13.8 MB, less than 33.33% of Python online submissions for Task Scheduler.