# Leetcode 101 Symmetric Tree 判断一棵树是否对称
题目描述：

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3
But the following [1,2,2,null,3,null,3] is not:

    1
   / \
  2   2
   \   \
   3    3


思路：

    1.（做法来自讨论区）判断一棵树是否是左右对称的，只需要判断它的左右孩子是互为镜面的，而这样的两棵树的镜面判断可以极为轻松地化为两棵树的判等问题（只不过左=左需要变成左=右）参见Leetcode 100，看来leetcode把这两道题放在一起是良苦用心啊

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
    bool isSymmetric(TreeNode* root)   
    {return isMirror(root, root);}  
  
    bool isMirror(TreeNode* p, TreeNode *q)   
    {  
        if(!p && !q) return true;  
        if((!p && q) || (p && !q)) return p==q;  
        return ((p->val == q->val) && isMirror(p->right, q->left) && isMirror(p->left, q->right));  
    }  
};  
```
