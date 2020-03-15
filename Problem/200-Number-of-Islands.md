## 200 Number of Islands

### *Description*

```
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

Input:
11110
11010
11000
00000

Output: 1
Example 2:

Input:
11000
11000
00100
00011

Output: 3
```



有点图论的感觉了，只要周围有土地，就可以合成一块岛，所以每一个节点都需要和四周的比对一下

现在比较重要的是，如何遍历整个地图，是否能够从左到右、从上到下的方法遍历



### *Answer from LeetCode*

LeetCode网站上的答案成功解决了如何不去重复地遍历地图。直接粗暴地把遍历过的地方变为0，是island的地方设置为1

这是第一个用Java写的程序

```java
class Solution {
    public int numIslands(char[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;
        int numOfIslands = 0;
        for(int i = 0;i<grid.length;i++){
            for(int j=0; j<grid[i].length; j++){
                if(grid[i][j] == '1'){
                    numOfIslands++;
                    dfs(grid, i, j);
                }
            }
        }
        return numOfIslands;
    }
    
    public void dfs(char[][] grid, int row, int col){
        if(row < 0 || row >= grid.length || col < 0 || col >= grid[row].length || grid[row][col] == '0'){
            return;
        }
        grid[row][col] = '0';
        dfs(grid, row-1, col);
        dfs(grid, row+1, col);
        dfs(grid, row, col-1);
        dfs(grid, row, col+1);
        return;
    }
}
```



### *Result*

Runtime: 1 ms, faster than 99.98% of Java online submissions for Number of Islands.

Memory Usage: 42.1 MB, less than 31.63% of Java online submissions for Number of Islands.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/312285329/) | 1 ms    | 42.1 MB | java     |
| 17 hours ago      | [Accepted](https://leetcode.com/submissions/detail/312099787/) | 1 ms    | 42.2 MB | java     |