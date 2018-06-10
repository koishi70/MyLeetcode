# Leetcode 69 Sqrt(x) 求x开根号的整数部分
题目描述：

Implement int sqrt(int x).

Compute and return the square root of x.

x is guaranteed to be a non-negative integer.

Example 1:

Input: 4
Output: 2
Example 2:

Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we want to return an integer, so 2
给出x平方根的整数部分

思路：

    1.为了加速这个过程，需要用到一定的magic number，过程采用二分查找，即从0，sqrt(INT_MAX)+1开始二分查找。

    2.如果最后没有找到恰好的平方根整数，那么根据mi*mi和x的位置返回mi或者mi-1，代码注释很清楚，可以自己琢磨

    3.这个解法可以很轻松地改成求立方根，四次方根等等

代码：

```
class Solution {  
public:  
    int mySqrt(int x)   
    {  
        int lo=0,hi=46341,mi;//46341=sqrt(INT_MAX)+1;  
        while(lo<hi)  
        {  
            mi=(lo+hi)>>1;  
            if(mi*mi<x) lo=mi+1;  
            else if(mi*mi>x) hi=mi;  
            else return mi;  
        }  
        //if not found  
        if(mi*mi<x) return mi;  //(mi-1)        (mi)(x here)(mi+1)  
        else return mi-1;       //(mi-1)(x here)(mi)        (mi+1)  
    }  
};  
```
