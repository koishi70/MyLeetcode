# Leetcode 83 Remove Duplicates from Sorted List 有序链表去重
题目描述：

Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.

思路：

    1.简单暴力，下一个数和本数相同，那么就本数的next指向下下一个数

    2.时间复杂度O（n）

    3.注意边界

代码：

```
/** 
 * Definition for singly-linked list. 
 * struct ListNode { 
 *     int val; 
 *     ListNode *next; 
 *     ListNode(int x) : val(x), next(NULL) {} 
 * }; 
 */  
class Solution {  
public:  
    ListNode* deleteDuplicates(ListNode* head)   
    {  
        ListNode* cur = head;  
        while(cur !=NULL && cur->next!=NULL)  
        {  
            if(cur->val == cur->next->val)  
                cur->next = cur->next->next;  
            else   
                cur = cur->next;  
        }  
        return head;     
    }  
};  
```
