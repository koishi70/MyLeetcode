# Leetcode 104 Maximum Depth of Binary Tree 二叉树的最大深度
题目描述：

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

For example:
Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
return its depth = 3.

给出一棵二叉树，求最大深度（从根开始计算）

思路：

    1.对于整棵树的深度计算可以化为两步：1.求左右子孩子的深度 2.取两个孩子的最大的深度+1。从而将大问题化为局部的求解

    2.时间复杂度O（n）

代码只有一行即可，极为简洁：

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
    int maxDepth(TreeNode* root)   
    {  
        return root==NULL ? 0 : max(maxDepth(root->left),maxDepth(root->right))+1;  
    }  
};  
```
