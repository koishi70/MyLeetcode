# Leetcode 21 Merge Two Sorted Lists 将两个已排序的链表合并起来
题目描述：

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

把两个已经排序的链表合并起来，合并后仍然要有序


Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
思路：

    把总的合并化成两个节点之间的合并。如果一个节点不存在，返回另一个节点。如果两个节点都存在，小的节点的next指向大的节点，返回小的节点指针。

    时间复杂度O（n），空间复杂度O（1）

源代码：

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2)  
    {  
        if (!l1) return l2;  
        if (!l2) return l1;  
        if (l1->val < l2->val)   
        {  
            l1->next = mergeTwoLists(l1->next, l2);  
            return l1;  
        }  
        else   
        {  
            l2->next = mergeTwoLists(l1, l2->next);  
            return l2;  
        }  
    }  
};  
```
