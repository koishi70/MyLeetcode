# Leetcode 88 Merge Sorted Array 合并两个有序数组
题目描述：

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

给出两个有序数组，长度为m，n，将nums2的数合并到nums1中去，假设nums1数组够大，可以放下所有n+m个数。

思路：

    1.为了防止数据错误，必须从后向前开始复制。也就是：int i=m-1, j=n-1, k=m+n-1;分别指向nums1，nums2，nums1合并后的最后一个。

    2.很容易就写出 nums1[k--] = (nums1[i]>nums2[j]) ? nums1[i--]: nums2[j--]; 但是仍需要考虑边界条件

    3.数组合并会出现两种情况：

    nums1先用完，此时i=-1，此后nums2直接归入nums1的前面即可。

    nums2先用完，此时nums1前面也没必要修改了，可以结束。

    注：ums1，nums2同时用完不可能，两个是交替归入的，总有最后一个。

代码：

```
class Solution {  
public:  
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n)   
    {  
        int i=m-1, j=n-1, k=m+n-1;//均从后向前  
        while(j>=0)//只要nums2没有用完，就可以继续，如果用完了，那么说明nums1前面的部分也不用改了  
        {  
            nums1[k--] = (i>=0 && nums1[i]>nums2[j]) ? nums1[i--]: nums2[j--]; // 注意，可能出现nums1用完的情况（i=-1）此时将剩下的nums2加上  
        }  
    }  
};  

    ```
