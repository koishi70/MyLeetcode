# Leetcode 66 Plus One
题目描述：

Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

用数组的方式表示一个很大的数字，将之++，比如[9,9,9]->[1,0,0,0]

思路：

    1.从后往前遍历这个数组，如果遇到了进位的数字9，那么本位改成0，如果遇到了0-8的数字，那么这一位++，权当进位了。如果输入类似于[9,9,9]->[1,0,0,0]，那么在这之后会变成[0,0,0]，强行在后面加一个0，首位改成1即可。

    2.时间复杂度O（n），空间复杂度O（1）

代码：
```
class Solution {  
public:  
    vector<int> plusOne(vector<int>& digits)   
    {  
        for (int i = digits.size() - 1; i >= 0; --i)  
        {  
            if (digits[i] == 9)  
                digits[i] = 0;  
            else  
                {  
                    digits[i]++;  
                    return digits;  
                }  
        }  
        //类似于999999999999的情况  
        digits[0] =1;  
        digits.push_back(0);  
        return digits;  
    }  
};  
```
