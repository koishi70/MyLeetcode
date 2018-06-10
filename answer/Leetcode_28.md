# Leetcode 28 Implement strStr() 字符串匹配
题目描述：

Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:

Input: haystack = "hello", needle = "ll"
Output: 2
Example 2:

Input: haystack = "aaaaa", needle = "bba"
Output: -1
    题目本质上是给出一个文本串haystack，模式串needle，求文本串中第一次出现了模式串的位置，匹配失败就返回-1，其实就是字符串匹配问题。

思路：

    1.暴力匹配即可，我想这个代码应该背下来，我从邓俊辉老师的数据结构书上看到了最好背的暴力匹配算法，在此直接给出。

    2. 匹配位置始终是i-j，文本串指针i，模式串指针j。匹配成功时，ij后移。匹配失败时i回退（i-=j），文本串i可以往后判断i++，j归零，从头开始。

    3.判断的时候：如果到最后都没匹配上，那么i-j>=n；如果在末尾匹配上了一部分（比如"apple"+"leaf"），并未完成，那么就有n-(i-j)<m。这都是匹配失败。

代码：

   

```
class Solution {  
public:  
    int strStr(string haystack, string needle)   
    {  
        int n=haystack.size(),  i=0;  
        int m=needle.size(),    j=0;  
        if(m==0) return 0;  
        if(n<m) return -1;  
        while(i<n && j<m)  
        {  
            if(haystack[i]==needle[j])  
                {i++;j++;}  
            else {i-=j;i++;j=0;}  
        }  
        if(i-j>=n || n-(i-j)<m) return -1;  
        return i-j;  
    }  
};  
```
