# Leetcode 7 Reverse Integer 将整数逆转
题目描述：

Given a 32-bit signed integer, reverse digits of an integer.

给一个int整数，将数字部分反转，符号不变，翻转后溢出则返回0

思路：

1.利用string作为中转，反转数字

2.保证函数总是反转x的绝对值，减少判断。

3.最开始将所有的末尾0去掉（除以10即可），免得翻转后开头出现0

4.时间复杂度O（lgn），空间复杂度O（lgn），n为输入数字，lgn即为输入数字的长度

源代码：

```
class Solution {  
public:  
    int reverse(int x) //只翻转一个正数  
    {  
        if(x==INT_MIN || x==0) return 0;//超出范围或者0，返回0  
        if(x<0) return -1*reverse(-1*x);//负数的话返回负的绝对值反转  
          
        while(x%10==0) //去掉末尾的0  
            x/=10;  
          
        string normal=to_string(x),reverse_str;//用string作为中转  
        int len=normal.size();  
        for(int i=len-1;i>=0;i--)  
            reverse_str+=normal[i];  
        long ans=stol(reverse_str,0,10);  
          
        if(ans>=INT_MAX) return 0;  
        else return (int)ans;  
    }  
};  
```
