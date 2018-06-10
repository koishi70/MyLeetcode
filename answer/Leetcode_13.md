# Leetcode 13 Roman to Integer 罗马数字转整数
题目描述：

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

将一段string的罗马数字转换到整数，输入数字在1-3999之间

思路：

1.原来的思路十分麻烦，需要匹配大量的情况，但是看到讨论区的大神的代码后瞬间佩服的五体投地，再也不敢把自己的代码放出来了

2.罗马数字的记载方法是这样的，从一到十，分别是I,II,III,IV,V,VI,VII,VIII,IX,X，经过仔细观察可以发现：在五，十等等数字前后可能出现I，在前面出现的I表示数字要减去这个一，在后面出现I表示数字要加上一，因此从左到右扫一遍数字，如果下一个比本罗马字小，那么加上去，比如VI=5+1。反之，要减掉，比如IV=-1+5

3.时间复杂度O（n），空间复杂度O（1）

源代码：

```
class Solution {  
public:  
int roman(char c) {  
    switch(c)   
    {  
        case 'I':  
            return 1;  
        case 'V':  
            return 5;  
        case 'X':  
            return 10;  
        case 'L':  
            return 50;  
        case 'C':  
            return 100;  
        case 'D':  
            return 500;  
        case 'M':  
            return 1000;  
        default:  
            return 0;  
    }  
}  
int romanToInt(string s) {  
    int sum = 0,i=0;  
    while(s[i])   
    {  
        int cur = roman(s[i]), next = roman(s[++i]);  
        if(cur<next) sum-=cur;  
        else sum+=cur;  
    }  
    return sum;  
}   
};  
```
