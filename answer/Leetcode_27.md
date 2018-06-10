# Leetcode 27 Remove Element
题目描述：

Given an array and a value, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:

Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.
给出一个数组，删除其中的等于val元素，注意，需要就地删除，返回新的数组长度。

思路：

    1.从头往后，遇到是val的元素，新的数组长度newn不增加，因为这个元素也不可能放到去重数组里，此后遇到新的数字直接覆盖之。

    2.遇到不是val的元素，将这个值放到新数组那里去，newn往后增长一个。

    3.正确性：由于出现了目标val元素要删掉，可以保证newn<=n，元素始终是要么原地不动，要么从后往前移动的，因此数组不会遇到数据丢失的问题。

代码：

```
class Solution {  
public:  
    int removeElement(vector<int>& nums, int val)   
    {  
        int n=nums.size(),newn=0;  
        for(int i=0;i<n;i++)  
            if(nums[i]!=val)   
                nums[newn++]=nums[i];  
        return newn;  
    }  
};  
```
