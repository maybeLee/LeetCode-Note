## 75 Sort Colors

### *Description*

```
Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

Example:

Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
Follow up:

	A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with 	total number of 0's, then 1's and followed by 2's.
Could you come up with a one-pass algorithm using only constant space?
```



### *My Solution I*

写了一个非常trash 的代码，大概的思路就是count list中的全部内容，然后再对数组进行重写

```java
class Solution {
    public void sortColors(int[] nums) {
        int count0 = 0;
        int count1 = 0;
        int count2 = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] == 0){
                count0++;
            }
            else if(nums[i] == 1){
                count1++;
            }
            else if(nums[i] == 2){
                count2++;
            }
        }
        for(int i = 0; i < nums.length; i++){
            if(count0!=0){
                nums[i] = 0;
                count0--;
            }
            else if(count1 != 0){
                nums[i] = 1;
                count1--;
            }
            else if(count2 != 0){
                nums[i] = 2;
                count2--;
            }
        }
    }
}
```



这种方法比较垃圾的地方在于，原先的数组地址都被浪费了

#### *Result*

Runtime: 0 ms, faster than 100.00% of Java online submissions for Sort Colors.

Memory Usage: 37.9 MB, less than 5.51% of Java online submissions for Sort Colors.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/312289383/) | 0 ms    | 37.9 MB | java     |
| 5 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/312288537/) | 0 ms    | 37.8 MB | java     |
| 5 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/312288508/) | 0 ms    | 38 MB   | java     |



### *My Solution II*

采用双指针的方法，颜色一共有三种，0，1，2，如果遇到2，就把2放在最后面，遇到0就把0放在最前面

```java
class Solution {
    public void sortColors(int[] nums) {    
        //two pointers
        //Define start and end pointers
        int start = 0;
        int end = nums.length - 1;
        
        for(int p=0; p <= end; p++){
            if(nums[p] == 0){
                if(start != p){
                    nums[start] = nums[p];
                    nums[p] = 1;
                }
                start++;
            }else if(nums[p] == 2){
                nums[p] = nums[end];
                nums[end] = 2;
                end--;
                p--;
            }
        }
    }
}
```



#### *Result*

Runtime: 0 ms, faster than 100.00% of Java online submissions for Sort Colors.

Memory Usage: 38.3 MB, less than 5.51% of Java online submissions for Sort Colors.



......搞不懂了......明明没有用什么内存.....