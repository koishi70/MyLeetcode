# Leetcode 53 Maximum Subarray 最大子串和
题目描述：

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

寻找nums数组中最大的子串和，返回和。

思路：

    1. 从头到尾遍历一次数组，每一次都向sum加上下一个数字，更新最大和ans

    2.之后做sum=max(sum,0);这一步可以理解为：（1）如果数组中全都是负数，那么所有的负数都不应该在sum中被累加，sum应当清零，此时ans应当保存所有负数中最大的那个。（2）如果数组中全都是正数，那么无所谓。（3）如果数组中正负混杂，那么如果sum在往正走了走以后最终跌破0，sum就不应当继续累加下去了，因为数组中至少还有一个正数比这些累加更大。（4）在以上的环节中，ans不断更新最大的和。

    3.时间复杂度O（n），空间复杂度O（1）

代码：

```
class Solution {  
public:  
    int maxSubArray(vector<int>& A)   
    {  
        int ans=A[0],i,j,sum=0;  
        for(i=0;i<A.size();i++)  
        {  
            sum+=A[i];  
            ans=max(sum,ans);  
            sum=max(sum,0);  
        }  
        return ans;  
    }  
};  
```
