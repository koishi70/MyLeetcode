# Leetcode 58 Length of Last Word 句子中最后一个词的长度
题目描述：

Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

Example:

Input: "Hello World"
Output: 5
思路：

    1.从后往前，先跳过末尾的空格，再数字母的个数

    2.时间复杂度O（n），n是句子长度，最差情况下句子末尾全都是空格，比如“apple                         ”，此时就需要遍历整个句子。

代码：
```
class Solution {
public:
    int lengthOfLastWord(string s) 
    {
        int n=s.size(),ans=0,i=n-1; 
        while(s[i]==' ')              
            i--;
        while(i>=0  && s[i] != ' ')
        {
            ans++;i--;
        }
        return ans;
    }
};
```
