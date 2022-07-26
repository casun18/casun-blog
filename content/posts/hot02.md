---
title: "Hot02"
subtitle: "2、两数相加"
date: 2022-07-25T18:16:29+08:00
author: "casun"
comment: false
weight: 0

tags: ["Mid","链表"]
categories:
- Hot100

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []

# See details front matter: /theme-documentation-content/#front-matter
---
## 2、两数相加
<!--more-->
# 1、题目
[2.两数相加](https://leetcode.cn/problems/add-two-numbers/)

给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。
![](/img/liangshuzhihe.png)

# 2、思路

注意进位

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    flag := 0
    var l *ListNode
    p := l
    for l1 != nil || l2 != nil {
        a := 0
        b := 0
        if l1 != nil {
            a = l1.Val
            l1 = l1.Next
        }
        if l2 != nil {
            b = l2.Val
            l2 = l2.Next
        }
        val := a + b + flag
        flag = val / 10
        tmp := &ListNode{Val:val % 10}
        p.Next = tmp
        p = p.Next
    }
    if flag > 0 {
        tmp := &ListNode{Val:flag}
        p.Next = tmp
    }
    return l.Next
}
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int flag = 0;
        ListNode l = new ListNode(-1);
        ListNode p = l;
        while(l1 != null && l2 != null) {
            int a = l1.val;
            int b = l2.val;
            int val = (a + b + flag)%10;
            flag = (a + b + flag) / 10;
            //System.out.printf("%d %d\n",val,p.val);
            ListNode tmp = new ListNode(val);
            p.next = tmp;
            p = p.next;
            l1 = l1.next;
            l2 = l2.next;
        }
        while(l1 != null) {
            int a = l1.val;
            int val = (a + flag) % 10;
            flag = (a + flag) / 10;
            ListNode tmp = new ListNode(val);
            p.next = tmp;
            p = p.next;
            l1 = l1.next;
        }
        while(l2 != null) {
            int a = l2.val;
            int val = (a + flag) % 10;
            flag = (a + flag) / 10;
            ListNode tmp = new ListNode(val);
            p.next = tmp;
            p = p.next;
            l2 = l2.next;
        }
        if(flag != 0) {
            ListNode tmp = new ListNode(flag);
            p.next = tmp;
        }
        return l.next;
    }
}
```