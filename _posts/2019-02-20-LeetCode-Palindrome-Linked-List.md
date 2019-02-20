---
layout: post
title:  "LeetCode 234. Palindrome Linked List"
date:   2017-07-20 16:36:18 +0800
categories: tutorial
---

题目链接：https://leetcode.com/problems/palindrome-linked-list/

这道题很简单，就是判断链表中的数字是否回文序列。用栈的话，轻松通过，但是消耗很大的内存，而且题目也明确暗示你能否用O(1)的空间复杂度：

![Time](/images/leetcode234.png "time")

这道题让我复习了快慢指针，并让我学到了逆序链表的操作。

## 快慢指针

快慢指针就是设置两个指针，慢的每次走一步，快的每次走两步。当快的抵达终点时，慢指针正好处在中间位置。如果你有经验，你就知道这道题目该怎么做了。：）

## 逆序链表

不借助栈，只借助3个多余的指针来完成逆序链表。代码够精炼的话，借助的指针数量可小于3。

参考：https://mp.weixin.qq.com/s/JbtCr9LAGYPyXZlnFO-bhw

## 我的代码

Runtime: 24 ms, faster than 98.57% of C++ online submissions for Palindrome Linked List.

Memory Usage: 12.4 MB, less than 90.62% of C++ online submissions forPalindrome Linked List.

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
        bool isPalindrome(ListNode* head) {
            if(!head)return true;
            
            ListNode* slow = head;
            ListNode* fast = head;

            while( fast->next && fast->next->next ){
                slow = slow->next;
                fast = fast->next->next;
            }

            // 判断链表个数是奇数还是偶数
            bool flag = false;
            if(fast->next==NULL) {
                flag = true;
            }

            //cout<<"slow "<<slow->val<<endl;
            //cout<<"fast "<<fast->val<<endl;


            ListNode * m1 = slow;
            ListNode * m2 = NULL;

            if(slow->next){
                m2 = slow->next;
            }
            m1->next = NULL;

            // 逆转前半部分链表
            ListNode * p1 = head;
            ListNode * p2 = p1->next;
            ListNode * p3 = NULL;
            while(p2){
                p3 = p2->next;
                p2->next = p1;
                p1 = p2;
                p2 = p3;
            }
            head->next = NULL;
            head = p1;

            //比较
            if(flag) {
                m1 = m1->next;
            }
            bool res = true;
            while(m1 && m2){
                //cout<<m1->val<<"  "<<m2->val<<endl;
                if(m1->val != m2->val){
                    res = false;
                    break;
                }
                m1 = m1->next;
                m2 = m2->next;
            }

            return res;
        }
    };