## 11 Container With Most Water

### *Description*

Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate $(i, a_i)$. *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

 

![img](../assets/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

 

**Example:**

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```



记得之前看lucifer的话，是双指针方法，这种方法好像不行，比如说[2,3,4,5,18,17,6]就不适用，指针的判断移动方法不能看大的那一条边，而是看小的那一条边，如果两个边的最小值能够动，就移动，不然就不动

### *My Solution*

这道题目的trick在于，究竟是挪低指针还是高指针，这取决于那一边更低，比如说，现在容器左侧是2，右侧是5，那挪右侧的5肯定没有效果，因为是2决定了容量，所以应该挪左侧，根据这种想法来决定每次挪哪一个，然后挪完进行一个判断是否更新最大容量。

#### *Code*

```python
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        #Solution I: two pointers
        low = 0
        high = len(height)-1
        maxSpace = min(height[low],height[high])*(high-low)
        while low < high:
            if height[low] > height[high]:
                high -= 1
                if height[high] > height[high+1]:
                    space = min(height[high], height[low])*(high-low)
                    if space > maxSpace:
                        maxSpace = space
            if height[high] >= height[low]:
                low += 1
                if height[low] > height[low-1]:
                    space = min(height[high], height[low])*(high-low)
                    if space > maxSpace:
                        maxSpace = space
                        
        return maxSpace
```



#### *Result*

Runtime: 108 ms, faster than 55.31% of Python online submissions for Container With Most Water.

Memory Usage: 13.1 MB, less than 44.07% of Python online submissions for Container With Most Water.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/307615977/) | 108 ms  | 13.1 MB | python   |
| 2 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/307615478/) | 108 ms  | 13.1 MB | python   |
| 2 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/307615431/) | 104 ms  | 13.1 MB | python   |



代码写得很蠢，之所以蠢是因为我算space的位置放错了，应该到了下一个循环再算space，而不是先算space再到下一个循环

改进：

```python
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        #Solution I: two pointers
        low = 0
        high = len(height)-1
        maxSpace = 0
        while low < high:
            maxSpace = max(maxSpace,min(height[high], height[low])*(high-low))
            if height[low] > height[high]:
                high -= 1
            else:
                low += 1
                        
        return maxSpace
```

