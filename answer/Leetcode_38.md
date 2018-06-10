# Leetcode 38 Count and Say
题目描述：

The count-and-say sequence is the sequence of integers with the first five terms as following:

1.     1
2.     11
3.     21
4.     1211
5.     111221
1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.

Given an integer n, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

Example 1:

Input: 1
Output: "1"
Example 2:

Input: 4
Output: "1211"


    输入一个数字n，根据规律输出对应的数列，这个数列是从n-1的数列得到的，具体规则是：数上个数列的数字，11数做21，即两个1，如此类推。

思路：

    1.首先n数列需要得到n-1数列，那么这个问题就可以一直减而治之到n=1,2的情况去。只需要专注做好从n-1到n的数列构造即可

    2.count从1开始数，遇到相同的数字count++，直到遇到不同的数字或者到末尾了，此时在答案末尾加上“几个几”

  代码：

```
class Solution {  
public:  
    string countAndSay(int n)   
    {  
        if (n == 1) return "1";  
        if (n == 2) return "11";  
        string result = countAndSay(n-1);  
        string newresult = "";  
          
        int count = 1;  
        for(int i = 1; i < result.size(); ++i)  
        {  
            if(result[i]!=result[i-1])  
            {  
                newresult.push_back('0'+count);newresult.push_back(result[i-1]);  
                count = 1;  
            }  
            else   
                count++;  
              
            if(i == result.size()-1)  
                {newresult.push_back('0'+count);newresult.push_back(result[i]);}  
        }  
        return newresult;  
    }  
};  
```
