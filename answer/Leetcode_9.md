# Leetcode 9 Palindrome Number 判断一个数是否为回文数
题目描述：

Determine whether an integer is a palindrome. Do this without extra space.

判断一个数是否是回文数（正着读和反着读一样），负数没有回文数

思路：

1.取a=输入数。令b=0，是a的倒转形式

每次b乘以10，以表示b向左移动一次，取a的最后一位数字加到b中，做完后a除以10，表示下一次可以取出a 的左面一位。

假设a=121，那么有：a=121，b=0 --> a=12，b=1 --> a=1，b=12 --> a=0，b=121

2.时间复杂度和空间复杂度都为O（lgn），lgn是输入数字的长度

源代码：

```
class Solution {  
public:  
    inline bool isPalindrome(int x)   
    {  
        if(x<0)    return false;  
        int a=x,b=0;//a正常的x，b回文的x  
        while(a)  
        {  
            b=10*b+a%10;  
            a=a/10;  
        }  
        return b==x;  
    }  
};  
```
