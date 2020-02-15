## 406 Queue Reconstruction by Height

### *Description*

```
Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers (h, k), where h is the height of the person and k is the number of people in front of this person who have a height greater than or equal to h. Write an algorithm to reconstruct the queue.

Note:
The number of people is less than 1,100.

 
Example

Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```



### *My Solution*

这道题我感觉可以用动态规划做？但是我没有那么做，我的想法是，这道题既然是要根据之前节点的大小数来排列，不妨就先把列表根据height(第一个元素)从大到小排个序，之后的可能会好处理一点，抱着这样的想法我先在草稿纸上把列表排个序看一下能得到什么：

```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Reverse:
[[7,0], [7,1]， [6,1], [5,0], [5,2], [4,4]]
#注意，[5,0]和[5,2]的顺序应该是[5,0]在前面，因为题目要求的是计算前面身高大于或等于自己的，因此既然最终结果就是[5,0]在前面，现在直接这么分会方便很多
#同时这也出来一个规律，如果前面的height大于等于后面的height，后面的那一个的k一定比前面的k多一个1
```

reverse完了之后，对list进行一个遍历，主要就是看，遍历的`node[1]`是否跟它所在的位置 `i`相等。如果相等的话就不管它，如果不相等的话，就把它放到应该放的位置



#### *Code*

```python
class Solution(object):
    def reconstructQueue(self, people):
        """
        :type people: List[List[int]]
        :rtype: List[List[int]]
        """
        #First I will sort the queue bubble sort?
        for i in range(len(people)):
            for j in range(i, len(people)):
                if people[i][0] < people[j][0] or (people[i][0] == people[j][0] and people[i][1] > people[j][1]):
                    people[i],people[j] = people[j],people[i]
        #Second I will do an iteration and move
        for i in range(len(people)):
            if people[i][1] != i:
                node = people.pop(i)
                people.insert(node[1], node)
        return people
```

#### *Result*

Runtime: 796 ms, faster than 8.45% of Python online submissions for Queue Reconstruction by Height.

Memory Usage: 12 MB, less than 100.00% of Python online submissions for Queue Reconstruction by Height.



我的妈呀！！第一次Memory 击败100%的人！我这个方法是不是比较小众啊.......但是runtime确实太长了，毕竟sort那一块是O(N^2)，可能用quicksort会更好？Anyway 应该有别的办法（比如说动态规划或者贪心算法）

但是我这个算法代码很好写啊....而且也很简单

### *LeetCode Solution*

跟我的想法一样.....可能是我bubble sort 写得太烂了吧。。。。。

```python
class Solution(object):
    def reconstructQueue(self, people):
        """
        :type people: List[List[int]]
        :rtype: List[List[int]]
        """
        ret = [[]]*len(people)
        people.sort(key = lambda x: (x[0],-x[1])) 
        indices = [i for i in range(len(people))]
        for j,(_,pk) in enumerate(people):
            i = indices.pop(pk)
            ret[i] = people[j]
        return ret
```





#### *Result*

Runtime: 80 ms, faster than 74.93% of Python online submissions for Queue Reconstruction by Height.

Memory Usage: 12.1 MB, less than 88.89% of Python online submissions for Queue Reconstruction by Height.



Anyway, 这是我第一次很快的就想到非常好的答案！！！！