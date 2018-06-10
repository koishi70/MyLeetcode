# Leetcode 67 Add Binary 二进制加
题目描述：

Given two binary strings, return their sum (also a binary string).

For example,
a = "11"
b = "1"

Return "100".

用两个string表示大数，返回他们的和（也用string）

思路：

    1.不用想，这道题用string肯定是有坑的，很有可能输入的string很长，远远超过了long long的范围，将string转换成long long再返回去肯定不行。



    2.仿照加法器，这一位p由三部分构成：A[i],B[i],以及上一位的进位，三个加起来了后，p%2就是这一位的值，p/=2得到下一位的进位。由此往复

代码：

```
class Solution {  
public:  
    string reverse(string a)  
    {  
        string s=a;  
        int lo=0,hi=s.size()-1;  
        while(lo<hi)  
        {  
            char temp = s[lo];  
            s[lo]=s[hi];  
            s[hi]=temp;  
            lo++;hi--;  
        }  
        return s;  
    }  
    string addBinary(string a, string b)   
    {  
        string ans="";  
        int p = 0, i = a.size() - 1, j = b.size() - 1;  
        while(i >= 0 || j >= 0 || p == 1)  
        {  
            p += i >= 0 ? a[i --] - '0' : 0;  
            p += j >= 0 ? b[j --] - '0' : 0;  
            ans += char(p % 2 + '0');  
            p /= 2;  
        }   
        return reverse(ans);  
    }  
};  
```
