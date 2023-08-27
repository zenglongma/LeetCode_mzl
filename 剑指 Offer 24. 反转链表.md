\> Problem: [剑指 Offer 24. 反转链表](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/description/)



[TOC]



### 思路

> 解题思路

> 分为递归和非递归两种方式:
>
> 倒叙数组有两种方法，一种是递归的，一种是非递归的
>
> 具体实现的话有四种实现方式
>
> 非递归的方法:一种是使用类双指针（实际是3个指针）来将数组倒叙，从头到尾将箭头反向；另一种是使用头插法将数据重新插入一遍
>
> 递归的有两种，一种是用递归实现3指针，类似于非递归的双指针法；另一种是直接使用子递归实现，处理好父递归和子递归之间的关系即可





###  解题方法

> 解题方法

> 递归法
>
> > 1. 递归法分为父节点head 调用子递归并处理子递归之间的关系两步实现【注意要设定好分界值】**这个递归是从最后一个节点往前修改指向**
> > 2. 第二个递归法使用递归实现双指针法【pre cur 去实现改变方向】**这个递归是从第一个开始逐渐向后修改指向**
>
> 非递归法
>
> > 1. 使用双指针法，从前往后反向指针的指向，直至遍历到最后一个节点
> > 2. 使用头插法将每个节点重新插入到新的链表中，并将新链表的头指针返回【这里可以加一个头结点，防止空指针异常】





###  复杂度

#### 时间复杂度: 

> 使用递归法和非递归法都是$O(n)$
>

#### 空间复杂度: 

> 空间复杂度： 使用递归法的话，时间复杂度是$O(n)$ 使用非递归法空间复杂度是原地的，没有使用栈，$O(1)$



###  Code

```Java
package 链表;

import java.util.LinkedList;

import javax.xml.soap.Node;

//https://leetcode.cn/problems/reverse-linked-list/

public class _206_反转链表 {
	
	public static void main(String[] args) {
		ListNode list  =new ListNode(0);
		ListNode list1 =new ListNode(1);
		list.next=list1;
		ListNode list2 =new ListNode(2);
		list1.next=list2;
		ListNode list3 =new ListNode(3);
		list2.next=list3;
		ListNode list4 =new ListNode(4);
		list3.next=list4;
		list4.next=null;
		
		ListNode temp =list;
		while (temp!=null) {
			System.out.println(temp.toString());
			temp=temp.next;
		}
		list = Solution2(list);
		temp =list;
		while (temp!=null) {
			System.out.println(temp.toString());
			temp=temp.next;
		}
		System.out.println(list);
	}
	/**
	 * 这里是使用的循环非递归实现的链表翻转——使用的是双指针 直接从前往后改变next指向
	 * @param head
	 * @return
	 */
	public static ListNode Solution1(ListNode head) {
		if (head==null||head.next==null) {// 链表为空或者只有一个节点
			return head;// 
		}
//		ListNode prev= null;
//		ListNode cur =head;
//		ListNode temp= null;
//		while(cur!=null) {
//			temp = cur.next;
//			cur.next= prev;
//			prev=cur;
//			cur=temp;
//		}
		ListNode prev =null;
		ListNode cur = head;
		ListNode temp = head;// 用来暂存临时节点 保证链表不被断开
		
		while(cur !=null) {
			temp = cur.next;
			cur.next = prev;
			prev = cur;
//			cur = prev.next;// 这个时候prev.next 指向的是前一个节点 不会往后走 所以报错
			cur =temp;
		}
		
		return prev;
	}

	
	/**
	 * 使用递归 从第一个节点往后进行翻转 直到翻转到原来链表的最后一个节点
	 * 类似于双指针法
	 * 
	 */
	
	public static ListNode Solution3(ListNode head) {
		return reverse(null,head);//首次调用递归函数，实现head节点翻转，原head节点的next为空
	}
	
	private static ListNode reverse( ListNode prev,ListNode cur) {
		if (cur == null) {
			return prev;
		}// 最后的结束条件  相当于实现到链表尾部
		
		ListNode temp = cur.next;// 提前存储下后边的节点
		cur.next = prev;// 实现翻转
		prev = cur;// 链表后移
		cur =temp;
		return reverse(prev, cur);	
	}
	
	
	/**
	 *     //使用递归从后往前，先翻转最后一个节点，再往前翻转
	 * @param head
	 * @return
	 */
	public static ListNode Solution2(ListNode head) {
		if (head==null || head.next==null) {
			return head;
		}
		/**
		 * 这里先翻转第二个节点开始往后的链表，从后边往前边进行翻转  最后翻转原来链表的head 节点 指向空
		 */
		ListNode newhead = Solution2(head.next);// 所以这里一开始就调用递归函数
		//		在每一次解递归的时候，函数返回的值都是改变指向的newhead，newhead指向了原来的尾结点
		
		ListNode nextListNode =head.next;//head在上一次解递归完成后，指向前一个节点，来实现倒置
		nextListNode.next = head;
		head.next=null;
//    	head.next.next = head;
//    	head.next = null;		
		return newhead;
	}
	
	
	/**
	 * 使用新建一个节点的方式 结合头插法实现链表翻转
	 */
	
	public static ListNode Solution4(ListNode head) {
		if (head== null|| head.next == null) {
			return head;
		}
		ListNode newHeadListNode =null;// 创建一个新链表
		ListNode temp = head;
		while(head!=null) {
			temp=temp.next;// 在原来链表上进行后移
			head.next =newHeadListNode;
			newHeadListNode = head;
			head=temp;	
		}
		return newHeadListNode;
	}
}

```

