## 48 Rotate Image

### *Description*

```
You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Note:

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:

Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
Example 2:

Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

内心oz：要是能用numpy就好了

### *My Solution*

首先，我尝试了通过索引变换的方法，将一个二维矩阵的索引转换为一维列表的索引，通过mod的方法实现旋转，后来发现不行（浪费了我一个半小时）

接着就直接brute force了，这道题目要求在原来matrix所指的内存进行改动，但是我又要在运算中保留没有变换过的原数值，所以另外开辟了一个矩阵内存储存原来矩阵的值

接着就是二重循环

```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """
        #Brute Force
        matrix1 = [[0]*len(matrix[0]) for _ in range(len(matrix))]
        for i in range(len(matrix)):
            for j in range(len(matrix[i])):
                matrix1[i][j] = matrix[i][j]
        width = len(matrix[0])
        for i in range(len(matrix1)):
            for j in range(len(matrix)):
                matrix[j][width-i-1] = matrix1[i][j]
```



#### *Result*

Runtime: 16 ms, faster than 95.61% of Python online submissions for Rotate Image.

Memory Usage: 11.7 MB, less than 83.78% of Python online submissions for Rotate Image.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305126194/) | 16 ms   | 11.7 MB | python   |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/305126172/) | 20 ms   | 11.7 MB | python   |
| 3 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/305125709/) | 24 ms   | 11.7 MB | python   |
| 3 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/305125687/) | 20 ms   | 11.8 MB | python   |

Brute Force 的结果都能这么好？？？