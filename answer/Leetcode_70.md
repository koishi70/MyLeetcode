# Leetcode 70 Climbing Stairs 爬楼梯的方法（动态规划）
题目描述：

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.


Example 1:

Input: 2
Output:  2
Explanation:  There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps
Example 2:

Input: 3
Output:  3
Explanation:  There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
从楼梯最下面开始，每次可以爬1级或者2级，求爬到最上面的方法数

思路：

    1.典型的动态规划问题。辅助数组保存到这一级的方法数，显然ans[0]=ans[1]=1，之后每一级都有从下一级爬上来和下两极爬上来两种做法，即dp[i]=dp[i-1]+dp[i-2]

代码：

```
class Solution {  
public:  
    int climbStairs(int n)   
    {  
        int ans[100];  
        ans[0]=ans[1]=1;  
        for(int i=2;i<=n;i++)  
            ans[i]=ans[i-1]+ans[i-2];  
        return ans[n];  
    }  
};  
```
