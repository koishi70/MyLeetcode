# Leetcode 14 寻找字符串之间的最长前缀
题目描述：

Write a function to find the longest common prefix string amongst an array of strings.

有许多字符串，寻找他们之间的最长的公共前缀

思路：

1.将n个字符串的比较转化为2个之间的，n个之间的无非是两两比较得到结果的最小值

2.假设有m个字符串，每个字符串n长度，时间复杂度O（mn），空间复杂度O（1）

源代码：

```
class Solution {  
public:  
    int longest(string &s1,string &s2)  
    {  
        int l1=s1.size(),l2=s2.size(),i=0;  
        int lmin=(l1<l2)?l1:l2;  
        while(i<lmin)  
        {  
            if(s1[i]==s2[i]) i++;  
            else break;  
        }  
        return i;  
    }  
      
    string longestCommonPrefix(vector<string>& strs)   
    {  
        int strsize=strs.size();  
        if (strsize==0) return "";  
        int i=0,num=strs[0].size();  
        while(i<strsize-1)  
        {  
            num = min(num,longest(strs[i],strs[1+i]));  
            i++;  
        }  
        string answer="";  
        for(int j=0;j<num;j++)  
            answer+=strs[0][j];  
        return answer;  
    }  
};  
```
