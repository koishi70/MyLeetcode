# Leetcode 26 Remove Duplicates from Sorted Array 有序向量中的去重
题目描述：

Given a sorted array, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example:

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.
给一个有序的向量，其中有重复的元素，返回去重之后有多少元素。算法最好是就地的

思路：

    1.就是常规的去重算法。遍历一次数组，每一次判断本位置的数字nums[i]是否和上一位置的数字nums[i-1]相同，如果相同的话，除了向后移动指针（i++）外什么都不做。直到出现了不同的数字，将这个数字移动到直至目前所见到的去重数组末尾id处，同时去重数组可以增长一个。

    2.时间复杂度O（n），空间复杂度O（1）

代码：

```
class Solution {  
public:  
    int removeDuplicates(vector<int>& nums)   
    {  
        int n=nums.size();  
        if(n < 2) return n;  
        int id = 1;  
        for(int i = 1; i < n; i++)   
            if(nums[i] != nums[i-1])   
                nums[id++] =nums[i];  
        return id;  
    }  
};  
```
