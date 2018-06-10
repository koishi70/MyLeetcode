# Leetcode 35 Search Insert Position 二分查找插入数字位置
题目描述：

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example 1:

Input: [1,3,5,6], 5
Output: 2
Example 2:

Input: [1,3,5,6], 2
Output: 1
Example 3:

Input: [1,3,5,6], 7
Output: 4
Example 1:

Input: [1,3,5,6], 0
Output: 0
    给出一个有序数组，一个插入值，如果这个值已经存在了，那么返回他的位置，如果没有，返回它应当插入的位置。

思路：

    1.二分查找位置，代码背下来为佳。在[lo，hi）的区间中，mi会把这个区间拆成[lo，mi）  mi   [mi+1，hi）三个区间，之后根据大小判断取哪个区间即可。

    2.需要注意的是如果需要知道插入位置，可以再进行判断，是放在首位还是末尾？是否有一堆重复元素堆在了一起？

代码：

```
class Solution {  
public:  
    int searchInsert(vector<int>& nums, int target)   
    {  
        int n=nums.size();  
        int lo=0,hi=n-1,mi;  
        while(lo<hi)  
        {  
            mi=(lo+hi)>>1;  
            if(nums[mi]>target) hi=mi;  
            else if(nums[mi]<target) lo=mi+1;  
            else return mi;  
        }  
          
        //not found  
        if(target>nums[n-1]) return n;  
        else if(target<nums[0]) return 0;  
        else  
        {  
            int pos=mi;  
            while(pos<n)  
            {  
                if(nums[pos]<target) pos++;  
                else break;  
            }  
            return pos;  
        }  
    }  
};  
```
