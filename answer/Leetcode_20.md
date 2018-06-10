# Leetcode 20 Valid Parentheses 判断括号匹配
题目描述：

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

给出一系列括号，判断匹配与否，注意这里有小括号，中括号，大括号

思路：

1.典型的需要用到栈的括号匹配问题，每次遇到左括号( [ {等，都将之入栈；每次遇到右括号) ] }等，都从栈中弹出相对应的左括号，如果没有对应的或者栈空，则不匹配

2.时间复杂度O（n），空间复杂度O（n）

源代码：
```
class Solution {  
public:  
    bool isValid(string s)   
    {  
        int i=0;  
        if(s.size()<=1) return 0;  
        stack<char> st;char temp,top;  
        while(i<s.size())  
        {  
            if(st.empty()) {st.push(s[i]);i++;}  
            temp = (char)s[i];top=st.top();  
            switch(temp)  
            {  
                case')':if(top == '(') {st.pop();} else return 0;break;  
                case']':if(top == '[') {st.pop();} else return 0;break;  
                case'}':if(top == '{') {st.pop();} else return 0;break;  
                case'(':st.push('(');break;  
                case'[':st.push('[');break;  
                case'{':st.push('{');break;  
                default: return 0;  
            }  
            i++;  
        }  
        if(st.empty()) return 1;  else return 0;  
    }  
};  
```
