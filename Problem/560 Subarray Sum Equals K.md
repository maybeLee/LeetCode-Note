## 560 Subarray Sum Equals K

### *Description*

```
Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

Example 1:
Input:nums = [1,1,1], k = 2
Output: 2
Note:
The length of the array is in range [1, 20,000].
The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].
```



### *My Solution*

我猜测要用sliding windows，不知道这个是不是sliding windows的意思，我首先设一个length为1的窗口，起点在第一个元素，如果窗口内值的和>k，那么左侧右移，如果窗口内值的和<k，那么窗口右侧继续右移，直到遍历完全部的为止。

但是这种方法没有考虑到列表中存在负数的情况。

LeetCode给的三个方法都比较简单.......就拿其中一种说好了......通过两种循环得到：

#### *Code*

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        for(int start = 0;start < nums.length; start++){
            int sum = 0;
            for(int end = start; end < nums.length; end++){
                sum += nums[end];
                if(sum == k){
                    count ++;
                }
            }
        }
        return count;
    }
}
```

Runtime: 208 ms, faster than 21.49% of Java online submissions for Subarray Sum Equals K.

Memory Usage: 41.1 MB, less than 7.61% of Java online submissions for Subarray Sum Equals K.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/313889791/) | 208 ms  | 41.1 MB | java     |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/313889682/) | 211 ms  | 41.1 MB | java     |



### *Solution II: HashMap*

```java
class Solution {
    public int subarraySum(int[] nums, int k) {      
        int count = 0, sum = 0;
        HashMap < Integer, Integer > map = new HashMap < > ();
        map.put(0, 1);
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (map.containsKey(sum - k))
                count += map.get(sum - k);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```

Runtime: 11 ms, faster than 96.79% of Java online submissions for Subarray Sum Equals K.

Memory Usage: 42.4 MB, less than 5.43% of Java online submissions for Subarray Sum Equals K.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/313891892/) | 11 ms   | 42.4 MB | java     |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/313891818/) | 11 ms   | 41.9 MB | java     |