# Leetcode 100 Same Tree 判断两棵树相同
题目描述：

Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

给出两个二叉树，判断它们是否相同，包括形状和值都要相同


Example 1:

Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
Example 2:

Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
Example 3:

Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false

思路：

    1.把整棵树化成更小的局部判断，从而将大事化小，即只需要判断一个节点和它的左右孩子是否相同就可以了。

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
    bool isSameTree(TreeNode* p, TreeNode* q)   
    {  
        if(!p && !q) return true;//两个都没了  
        if((!p && q)||(p && !q)) return false;//如果有一个没了  
        return (p->val == q->val && isSameTree(p->left, q->left) && isSameTree(p->right, q->right));  
    }  
};  

```
