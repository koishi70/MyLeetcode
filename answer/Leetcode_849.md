# Leetcode 849 到最近的人的最大距离
问题描述：

在一排座位（ seats）中，1 代表有人坐在座位上，0 代表座位上是空的。

至少有一个空座位，且至少有一人坐在座位上。

亚历克斯希望坐在一个能够使他与离他最近的人之间的距离达到最大化的座位上。

返回他到离他最近的人的最大距离。

示例 1：

输入：[1,0,0,0,1,0,1]
输出：2
解释：
如果亚历克斯坐在第二个空位（seats[2]）上，他到离他最近的人的距离为 2 。
如果亚历克斯坐在其它任何一个空位上，他到离他最近的人的距离为 1 。
因此，他到离他最近的人的最大距离是 2 。 
示例 2：

输入：[1,0,0,0]
输出：3
解释： 
如果亚历克斯坐在最后一个座位上，他离最近的人有 3 个座位远。
这是可能的最大距离，所以答案是 3 。
提示：

1 <= seats.length <= 20000
seats 中只含有 0 和 1，至少有一个 0，且至少有一个 1。

算法：

1. 建立一个新数组，在两头加上1作为哨兵，求出这个新数组的最长连续0的大小len，显然，答案应该是(len+1)/2

2.如果两头没人坐的话，特别处理之，求出两头连续0的最大长度，最终答案应该是max(1中的答案，两头连续0的最大长度)

代码：

```
class Solution {  
public:  
    int maxDistToClosest(vector<int>& seats)   
    {  
        vector<int> new_seats;//左右两边都算成1，统一规划  
        new_seats.push_back(1);  
        for(int i=0;i<seats.size();i++)  
            new_seats.push_back(seats[i]);  
        new_seats.push_back(1);  
  
        int max_jiange=-1,temp=0;//求出最大的连续0长度  
        for(int i=0;i<new_seats.size();i++)  
        {  
            if(new_seats[i]==0)  
                temp++;  
            else  
            {  
                max_jiange = max(max_jiange,temp);  
                temp = 0;  
            }  
        }  
          
        if(seats[0]!=0 && seats[seats.size()-1]!=0)//不涉及到可能是坐在两头的情况  
            return int((max_jiange+1)/2);  
        else  
        {  
            int left_maxlen=0,right_maxlen=0;  
            int pos=0;  
            while(seats[pos]==0)    {pos++;left_maxlen++;}  
            pos=seats.size()-1;  
            while(seats[pos]==0)    {pos--;right_maxlen++;}  
            return max(int((max_jiange+1)/2),max(left_maxlen,right_maxlen));  
        }  
    }  
};  
```
