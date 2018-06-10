# Leetcode 108 Convert Sorted Array to Binary Search Tree 将一个有序数组变成BST
题目描述：

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.


Example:

Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
    给出一个有序的数组，将这个数组根据BST的定义，改成一棵二叉搜索树，即一个节点的左面的节点都是小于他的，右面的都是大于他的。

思路：

    1.根据定义，有序数组恰好是BST的中序遍历数组，将数组[lo,hi)从mi切分成3片，[lo,mi)  mi  [mi+1,hi)  （数组总是使用[a,b)表示，），分别是左孩子，根节点，右孩子，BST中，处处遵循这样的结构。

    2.时间复杂度O（n）

代码：

```
/** 
 * Definition for a binary tree node. 
 * struct TreeNode { 
 *     int val; 
 *     TreeNode *left; 
 *     TreeNode *right; 
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {} 
 * }; 
 */  
class Solution {  
public:  
    TreeNode* sortedArrayToBST(vector<int>& nums)   
    {  
        int n=nums.size(),mi=n>>1;//lo=0,hi=n,mi=(lo+hi)/2  
        if(n == 0) return NULL;  
        TreeNode* root = new TreeNode(nums[mi]);  
          
        vector<int> lnums(nums.begin(), nums.begin()+mi);  
        vector<int> rnums(nums.begin()+mi+1, nums.end());  
          
        root->left  = sortedArrayToBST(lnums);  
        root->right = sortedArrayToBST(rnums);  
  
        return root;  
    }  
};  

```
