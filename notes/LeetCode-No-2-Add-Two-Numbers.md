---
title: LeetCode No.2 Add Two Numbers
tags:
  - LeetCode
  - LinkedList
categories:
  - LeetCode
abbrlink: '271525e0'
date: 2019-12-16 14:53:21
---

# **From** 
1. [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/#/description)

<!-- more -->
# **Problem**


You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4) Output: 7 -> 0 -> 8


给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

## **EXAMPLES**

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807


来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/add-two-numbers
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。




# **Solutions**

首先应该 遍历两个 链表，将对应的值加起来后，插入新链表

将进位 +1的值 加到 后面的结点上

如果遍历之后还剩下 需要进位的值，需要将 进位值 加入到新的链表中，即增加 一个新结点

还要考虑边界情况： 

1. 链表1和链表2 同时为空，直接返回 “error"

2. 链表1和链表2 有一个为空， 则返回非空的那个

