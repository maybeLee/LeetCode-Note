## 338 Counting Bits

### *Description*

```
Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example 1:

Input: 2
Output: [0,1,1]
Example 2:

Input: 5
Output: [0,1,1,2,1,2]
Follow up:

It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
Space complexity should be O(n).
Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.
```



### *My Solution*

这个问题有一个窍门，如果num是奇数，那么num对应的值应该是num-1对应的值再加1，如果num是偶数就比较麻烦了

举个例子很容易理解

| num=3：011 | num-1=2：010 |
| ---------- | ------------ |
| num=7：111 | num-1=6：110 |
| num=2：10  | num-1=1：01  |
| num=4: 100 | num-1=3: 011 |

因此现在要解决的问题就是，如果是偶数的情况，如何判断前一个奇数对应的值应该加多少

这算是一个动态规划问题吧

#### *Code*

```python
class Solution(object):
    def countBits(self, num):
        """
        :type num: int
        :rtype: List[int]
        """
        if num == 0:
            return [0]
        total = [0]
        for i in range(1,num+1):
            if i % 2 != 0:  total.append(total[-1]+1)
            else:
                count = 1
                while True:
                    if (i>>count) % 2 != 0:  break
                    else:  count += 1
                total.append(total[-1]-count+1)
        return total
```



#### *Result*

Runtime: 80 ms, faster than 43.71% of Python online submissions for Counting Bits.

Memory Usage: 15.8 MB, less than 18.18% of Python online submissions for Counting Bits.



这一次的结果还算比较满意吧，尤其是581给了我太大的打击之后.........为啥内存占用这么多？我就用了一个list 啊，外加一个count 一个 i变量，这道题至少得用一个list的内存吧.....