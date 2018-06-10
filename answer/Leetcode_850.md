# Leetcode 850 矩形面积 II
题目描述：

我们给出了一个（轴对齐的）矩形列表 rectangles 。 对于 rectangle[i] = [x1, y1, x2, y2]，其中（x1，y1）是矩形 i 左下角的坐标，（x2，y2）是该矩形右上角的坐标。

找出平面中所有矩形叠加覆盖后的总面积。 由于答案可能太大，请返回它对 10 ^ 9 + 7 取模的结果。


![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/06/06/rectangle_area_ii_pic.png)
示例 1：

输入：[[0,0,2,2],[1,0,2,3],[1,0,3,1]]
输出：6
解释：如图所示。
示例 2：

输入：[[0,0,1000000000,1000000000]]
输出：49
解释：答案是 10^18 对 (10^9 + 7) 取模的结果， 即 (10^9)^2 → (-7)^2 = 49 。
提示：

1 <= rectangles.length <= 200
rectanges[i].length = 4
0 <= rectangles[i][j] <= 10^9
矩形叠加覆盖后的总面积不会超越 2^63 - 1 ，这意味着一个 64 为有符号整数可以用来保存面积结果。

算法：

![](https://img-blog.csdn.net/20180610105905653?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3l1d2VpbWluZzcw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

1.将所有矩形的y1y2收集起来，排序去重，得到一个all_y数组，这个数组就可以指示每一个最小的y间隔是多少。

2.对于每一个最小的y_min:y_max的范围，求出这个范围内有哪些矩形，收集这些矩形的x1x2

3.对于这些x1x2，求出这些x范围的并集所覆盖的长度sum_x

4.sum_x*y小区间的长度，加到答案里面去。

代码：
```
class Solution {  
public:  
    long long binji(vector<int> &xs)  
    {  
        int n=xs.size()/2;  
        long long ans=0;  
        vector<int> all_x(xs);  
        sort(all_x.begin(),all_x.end());  
        all_x.erase(unique(all_x.begin(), all_x.end()), all_x.end());//所有的x排序去重，得到了一系列最小的区间  
          
        for(int i=0;i<all_x.size()-1;i++)  
        {  
            int lo=all_x[i],hi=all_x[i+1];//对于一个极小区间来说，遍历一次xs，有的话加上去  
            for(int j=0;j<n;j++)  
            {  
                if(xs[2*j]<=lo && hi<=xs[2*j+1])  
                {  
                    ans += hi-lo;  
                    break;//已经在了，不必算其他的区间  
                }  
            }  
        }  
        return ans;  
    }  
    long long in_delta_y_area(vector<vector<int>>& rectangles,int y_min,int y_max)  
        //夹在y一定范围内的矩形的x都要加入一个列表，然后求出这些x的最大最小值  
    {  
        int n = rectangles.size();  
        vector<int> xs;//所有矩形在y范围内的那些x1x2们  
        for(int i=0;i<n;i++)  
        {  
            int x1=rectangles[i][0],y1=rectangles[i][1],x2=rectangles[i][2],y2=rectangles[i][3];  
            if(y1<=y_min && y_max<=y2)  
            {  
                xs.push_back(x1);  
                xs.push_back(x2);  
            }  
        }  
        if(xs.size()==0)  
            return 0;  
          
        long long sum_x =binji(xs);//对于这些x1x2的集合，求出集合并集覆盖区间  
        return sum_x*(long long)abs((long long)y_max-(long long)y_min);  
    }  
    int rectangleArea(vector<vector<int>>& rectangles)   
    {  
        int n = rectangles.size();  
        vector<int> all_y;//找到所有的y  
        for(int i=0;i<n;i++)  
        {  
            all_y.push_back(rectangles[i][1]);  
            all_y.push_back(rectangles[i][3]);  
        }  
        sort(all_y.begin(),all_y.end());  
        all_y.erase(unique(all_y.begin(), all_y.end()), all_y.end());//排序去重，得到最小的y的分割  
          
        long long ans=0;  
        for(int i=0;i<all_y.size()-1;i++)  
            ans += in_delta_y_area(rectangles,all_y[i],all_y[i+1]);//每个y的小区间都求一次x方向上的矩形之和  
          
        return ans % 1000000007;  
    }  
};  
```
