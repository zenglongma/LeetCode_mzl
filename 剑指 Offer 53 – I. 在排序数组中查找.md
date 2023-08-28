# 剑指 Offer 53 – I. 在排序数组中查找

\> Problem: [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/description/)



[TOC]



### 思路

> 解题思路

> 

###  解题方法

> 解题方法

> 1. 这里

###  复杂度

#### 时间复杂度: 

> 时间复杂度： $O(n+m)$
>
> m 和 n 分别是链表的长度



#### 空间复杂度: 

> 空间复杂度： $O(1)$



###  Code

```Java
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
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
  		ListNode p1= list1;
    	ListNode p2= list2;
    	
    	if (p1==null||p2==null) {// 两个链表中任意一个是空 则返回另一个链表的头结点
    		if (p1==null) {
    			return p2;
			}
			return p1;
		}
//     下边是两个链表都不为空的情况
//    	先找到两个链表中当前指针指向的较小的值，然后将其插入到新链表中，并将指针后移并不断重复，
//    	直到一个链表为空，然后将非空链表接到新链表尾部
    	ListNode list = new ListNode(0);// 新链表设定头结点，返回时返回头结点后边的一个节点
    	ListNode tempListNode =list;
//    	这里先将一个链表遍历完，并向新链表中进行插入数据
    	while ((p1!= null)&&(p2 != null)) {  		
			if (p1.val<=p2.val) {// 找两个指针指向的节点中较小的值
				tempListNode.next = p1;
				tempListNode=tempListNode.next;
				p1=p1.next;
			}else {
				tempListNode.next = p2;
				tempListNode=tempListNode.next;
				p2=p2.next;
			}
		}
    	//上边代码执行完 p1  和 p2 一定有一个是空的
    	tempListNode.next = p1== null ? p2 : p1;// 三目运算符 直接获得值
    	
    	
    	
//    	if (p1==null) {//说明p1 执行遍历完，需要将p2剩余的数据插入到新俩表后边
//    		tempListNode.next=p2;	
//		}else {
//			tempListNode.next=p1;	
//		}

    	
    	return list.next;

    }
}
```

