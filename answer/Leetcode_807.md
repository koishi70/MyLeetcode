# Leetcode 807 Max Increase to Keep City Skyline 不变天际线
题目描述：

In a 2 dimensional array grid, each value grid[i][j] represents the height of a building located there. We are allowed to increase the height of any number of buildings, by any amount (the amounts can be different for different buildings). Height 0 is considered to be a building as well. 

At the end, the "skyline" when viewed from all four directions of the grid, i.e. top, bottom, left, and right, must be the same as the skyline of the original grid. A city's skyline is the outer contour of the rectangles formed by all the buildings when viewed from a distance. See the following example.

What is the maximum total sum that the height of the buildings can be increased?

Example:
Input: grid = [[3,0,8,4],[2,4,5,7],[9,2,6,3],[0,3,1,0]]
Output: 35
Explanation: 
The grid is:
[ [3, 0, 8, 4], 
  [2, 4, 5, 7],
  [9, 2, 6, 3],
  [0, 3, 1, 0] ]

The skyline viewed from top or bottom is: [9, 4, 8, 7]
The skyline viewed from left or right is: [8, 7, 9, 3]

The grid after increasing the height of buildings without affecting skylines is:

gridNew = [ [8, 4, 8, 7],
            [7, 4, 7, 7],
            [9, 4, 8, 7],
            [3, 3, 3, 3] ]

Notes:

1 < grid.length = grid[0].length <= 50.
All heights grid[i][j] are in the range [0, 100].
All buildings in grid[i][j] occupy the entire grid cell: that is, they are a 1 x 1 x grid[i][j] rectangular prism.


翻译：

    1.给出一个城市矩阵，每个元素表示这个地方的大楼高度，一个城市具有从左到右，从上到下两个天际线，也就是从这个方向看去最高的那栋大楼构成的。

    2.提升每栋楼的高度，但是不能破坏天际线，求最大可以提升的高度（总和）

    3.显然grid[i][j]最高可以到min(水平天际线[i],垂直天际线[j])，遍历一次矩阵即可

代码：

```
class Solution {  
public:  
    vector<int> to_skyline_shuipin(vector<vector<int>>& grid,int n,int m)  
    {  
        vector<int> ans(m,INT_MIN);  
        for(int j=0;j<m;j++)  
            for(int i=0;i<n;i++)  
                ans[j]=max(ans[j],grid[i][j]);  
        return ans;  
    }  
    vector<int> to_skyline_chuizhi(vector<vector<int>>& grid,int n,int m)  
    {  
        vector<int> ans(n,INT_MIN);  
        for(int i=0;i<n;i++)  
            for(int j=0;j<m;j++)  
                ans[i]=max(ans[i],grid[i][j]);  
        return ans;  
    }  
    int maxIncreaseKeepingSkyline(vector<vector<int>>& grid)   
    {  
        int max_up=0,n=grid.size(),m=grid[0].size();  
        vector<int> shuipin = to_skyline_shuipin(grid,n,m);//从左往右看  
        vector<int> chuizhi = to_skyline_chuizhi(grid,n,m);//从上往下看  
        for(int i=0;i<n;i++)  
            for(int j=0;j<m;j++)  
                max_up += min(shuipin[j],chuizhi[i])-grid[i][j];  
        return max_up;  
    }  
};  
```
