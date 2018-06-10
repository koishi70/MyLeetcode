# Leetcode 107 Binary Tree Level Order Traversal II 二叉树层次遍历与倒转
题目描述：

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:

[
  [15,7],
  [9,20],
  [3]
]
给出一个二叉树，得到它的层次遍历的二维数组，然后把这个数组倒过来（就像倒金字塔一样）。

思路：

    1.层次遍历二叉树只需要化为两步：1.节点写入它所在的层中 2.对节点的左右孩子执行1（代码建议背）

    2.传递二维数组的引用，让计算更快。

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
    void levelOrder(vector<vector<int>> &ans, TreeNode *root, int level)   
    {  
        if (!root) return;  
        if (level >= ans.size())  
            ans.push_back({});  
          
        levelOrder(ans,root->left,level+1);  
        ans[level].push_back(root->val);  
        levelOrder(ans,root->right,level+1);  
    }  
  
vector<vector<int>> levelOrderBottom(TreeNode* root)   
    {  
        vector<vector<int>> ans;  
        levelOrder(ans,root,0);  
        reverse(ans.begin(),ans.end());  
        return ans;  
    }  
      
};  
```
