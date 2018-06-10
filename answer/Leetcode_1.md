# Leetcode 1 Two Sum 两数之和
# 题目描述：

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

给出一个数组，寻找这个数组中是否存在两个数，使得其和为目标target，返回这两个数的位置

保证数组中一定有所求的两个数，并且一个数只能够用一次。

思路一：

暴力算法，遍历所有的数对，时间复杂度O（n^2），空间复杂度O（1）

附代码：

```
class Solution {  
public:  
    vector<int> twoSum(vector<int>& nums, int target)   
    {  
        int n=nums.size();  
        for(int i=0;i<n;i++)  
            for(int j=i+1;j<n;j++)  
                if(nums[i]+nums[j]==target)  
                    return {i,j};  
    }  
};  
```

思路二：

1.从小到大排序这个数组，使用lo，hi两个指针，开始时分别指向位置0和最后一个数，计算它们的和sum。

        如果恰好得到target目标值，则返回答案。

        如果和小于target，那么为了得到更大的和sum，可以使lo++，让lo指向下一个更大的数，这样才有可能凑出更大的和sum，并得到目标和target。

        反之亦然，如果和大于target，那么为了得到更小的和sum，可以使hi--，指向下一个更小的数。

2.使用pair<int, int>来保存每个数的值以及位置，在排序后不至于无法寻找到其原来的位置。

3.时间复杂度O（nlgn），空间复杂度O（n）

附代码：

```
class Solution {  
public:  
    friend bool operator<(const pair<int,int> &a,const pair<int,int> &b)  
    {return a.first<b.first;}  
      
    vector<int> twoSum(vector<int>& nums, int target)   
    {  
        int lo = 0 , hi = nums.size() - 1;  
          
        vector<pair<int,int>> my_nums;  
        for(int i = 0 ; i < nums.size() ; i++)  
            my_nums.push_back( {nums[i],i} );  
          
        sort(my_nums.begin(),my_nums.end());  
          
        while(lo < hi)  
        {  
            int sum_temp = my_nums[lo].first+my_nums[hi].first;  
            if(sum_temp == target)  
                return {my_nums[lo].second,my_nums[hi].second};  
            if(sum_temp<target)   
                lo++;  
            else   
                hi--;  
        }  
    }  
};  
```
注意：

leetcode中：重载operator<用于pair的sort()函数需要在前面加上friend才行
