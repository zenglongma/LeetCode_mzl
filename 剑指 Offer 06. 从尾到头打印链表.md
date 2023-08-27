# 剑指 Offer 06. 从尾到头打印链表

\> Problem: [剑指 Offer 06. 从尾到头打印链表](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/description/)

> 用数组的形式，将所给的链表倒叙打印出来

[TOC]



### 思路

> 解题思路

> 倒叙的打印一个链表，这里可以从两个角度去考虑，第一个是对链表进行处理，将链表的数据进行翻转，然后在正序打印【反转链表】；第二个角度是将链表数据反向的复制出来，然后正序的打印【倒叙输出：考虑栈的作用以及倒叙遍历】；
>
> ![image-20230826210754091](../assets/image-20230826210754091.png)
>
> > ①数据先入栈，然后出栈就是倒顺序② ③先将链表进行倒叙【递归和非递归】，再讲数据正序打印 ④正序遍历使用两个数组暂存数据并倒叙输出数据 ⑤使用一个数组完成数据倒叙

###  解题方法

#### 解题方法1

> 1. 使用栈先进后出暂存数据并输出结果
> 2. 这里要确定好数据的个数，方便返回对应的大小的数组

```java

 /**
	  * 使用栈 先把链表数据存入到栈中，然后将数据从栈中弹出到数组中，直接返回即可
	  *    空间复杂度较低，时间复杂度较高
	  * @param head
	  * @return
	  */
	 public int[] reversePrint1(ListNode head) {

	      	Stack<Integer> Integers =new Stack<Integer>();
	      	if (head ==null) {
	      		return new int[0];
			}
	      	ListNode temp= head;
	      	int num = 0;
	      	while (temp != null) {
	      		Integers.add(temp.val);
	      		temp= temp.next;
	      		num++;
			}
	      	int a[]  = new int[num];
	      	for (int i = 0; i < num; i++) {
				a[i]=Integers.pop();
			}
	      	return a;
	 }
```



时间复杂度： $O(n)$

空间复杂度： $O(n)$



#### 解题方法2+3

##### 递归法

> **递归法**

> 将数组倒序，然后正序的遍历数组并写入到数组中
>
> 倒叙数组有两种方法，一种是递归的，一种是非递归的
>
> 具体实现的话有四种实现方式
>
> 非递归的方法:一种是使用类双指针（实际是3个指针）来将数组倒叙，从头到尾将箭头反向；另一种是使用头插法将数据重新插入一遍
>
> 递归的有两种，一种是用递归实现3指针，类似于非递归的双指针法；另一种是直接使用子递归实现，处理好父递归和子递归之间的关系即可



> 这里有个麻烦的点是在使用递归方法的时候，不能直接一次遍历查出数据的个数，需要再重新遍历一遍，并且使用递归增加了空间复杂度

```java

 /**
	  * 先将链表进行倒置，然后直接遍历进行数据写入新数组并返回【这里数组翻转可以有递归和非递归两种实现方式】
	  * 递归版
	  */
	 public static int[] reversePrint2(ListNode head) {
		 int num = 0;
		 head = reverseList(head);
		 ListNode temp = head;
//		 统计数量
		 while (temp!=null) {
			num++;
			temp =temp.next;
		 }

		 temp =head;
      	 int a[]  = new int[num];
      	 for (int i = 0; i < num; i++) {
      		 a[i] = temp.val;
      		 temp=temp.next;
		}
      	return a;
	 }
	 
	 public static ListNode reverseList(ListNode head) {
		if (head==null || head.next == null) {
			return head;			
		}

		ListNode tempListNode = reverseList(head.next);
		head.next.next = head;
		head.next = null;
		return tempListNode;
	}
	 
```

> 在上边代码中没有使用递归三指针倒叙法【不要求掌握】，掌握递归的一种方法即可



递归的空间复杂度与使用栈的空间复杂度是一致的，所以需要使用非递归的方法进行优化

时间复杂度： $O(n)$

空间复杂度： $O(n)$

##### 非递归法

> **非递归法**
>
> 使用非递归法的话，就是只需要改变一下链表倒叙的算法即可，正序打印链表的方法没有改变，跟上边一样

> 这里用两个指针，对链表进行倒叙的时候，老是习惯先将快指针和慢指针指向同一个地方，然后先让快指针走，这是错误的；应该在循环
>
> 之前就让慢指针指向null，让快指针指向head，直接进入循环的时候，先改变head指针的指向，在倒叙链表中其他元素的指向

```java
 /**
	  * 先将链表进行倒置，然后直接遍历进行数据写入新数组并返回【这里数组翻转可以有递归和非递归两种实现方式】
	  * 非递归版
	 */
	 public static int[] reversePrint3(ListNode head) {
		 
		 int num = 0;
		 head = reverseList1(head);
		 ListNode temp = head;
//		 统计数量
		 while (temp!=null) {
			num++;
			temp =temp.next;
		 }

		 temp =head;
      	 int a[]  = new int[num];
      	 for (int i = 0; i < num; i++) {
      		 a[i] = temp.val;
      		 temp=temp.next;
		}
      	return a;
	 }
	 
	 public static ListNode reverseList1(ListNode head) {
		 
		 if (head==null || head.next == null) {
			 return head;
		}
//		 都从头节点开始
		 ListNode temp = head;

		 ListNode preListNode = head;// 前指针
		 ListNode lastListNode = null;// 后指针
		 while (preListNode != null) {
//			 preListNode =temp;// 这个地方 一开始写三指针 还是会被卡主，想着先移动前指针  但是这里有一步是没在循环中执行的
//			 在循环外让前指针比后指针快一步,先让前指针指向head,而后指针指向null，方便更改head的指向，先让head指为null
			 temp = preListNode.next;
			 preListNode.next=lastListNode;
			 lastListNode = preListNode;
			 preListNode =temp;
		}
		 return lastListNode;
	} 

```

时间复杂度： $O(n)$

空间复杂度： $O(1)$

> 非递归倒叙链表的方式是原地的，所以空间复杂度比较低

#### 解题方法4+5

> 分别使用两个链表和使用一个链表对数组进行存储并倒叙的写入，正向遍历链表，然后倒叙的进行赋值设定
>
> 使用两个数组的时候，会将数组进行复制，也就是先正序的复制到一个数组中，在倒序的将数组复制到另一个数组中，实现将数据再倒叙的赋值
>
> 使用一个数组的时候，直接在遍历链表的时候，从后往前的写入到数组中，实现数组的数据倒叙



> 注意点:
>
> 1. 在使用数组的时候，要先弄清楚数据的个数，在申请空间
> 2. 数组的下标与数据个数相差1，所以要在写入的时候，先将数据个数-1 在写入到数组中

```Java
package day2;


import java.util.Stack;



public class 剑指Offer06从尾到头打印链表 {
	
	/**
 	*    下边的第一个方法使用的是用两个数组，第一个先遍历链表存储数据，并把该数组倒序复制到另一个数组中
 	*    空间复杂度较高，时间复杂度稍快.
	 * @param head
	 * @return
	 */
	 public int[] reversePrint0(ListNode head) {
	      	int a[]  = new int[10000];
	    	
//	    	int[] b = new int[100];//数组的另外一种定义方式

	    	if (head==null) {
	    		return new int[0];
			}
	    	ListNode temp = head;

	    	int i = 0;
	    	for (; temp != null; i++) {
				a[i] = temp.val;
				temp = temp.next;
			}
//	    	i=0;
//	    	while (temp != null) {
//	    		a[i] = temp.val;
//	    		i++;
//	    		temp = temp.next;
//			}
	    	int num = i;
	    	int[] b = new int[num];//数组的另外一种定义方式
	    	for (int j = 0; j < num; j++) {
				b[j] = a[i-1];// 这里获取数据的时候，坐标与数据序号差1
				i--;
			}
	    	
	    	return b;

	    }
	 
	 /**
	  * 对上边一个方法进行改进，不使用两个数组进行处理，直接用一个数组进行处理，在使用数组的时候进行倒叙的写入数组即可
	  */
	 public int[] reversePrint00(ListNode head) {
	    	if (head==null) {
	    		return new int[0];
			}// 特殊处理
	    	int num = 0;// 设定长度
	    	ListNode tempListNode =head;
	    	while (tempListNode!= null) {
	    		num++;
	    		tempListNode= tempListNode.next;				
			}
	      	int a[]  = new int[num];

	    	while (head!= null) {
	    		a[num-1] = head.val;
	    		head= head.next;
	    		num--;
			}
	      	return a;
	 }
	 
	 
	
	 
	
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
			int[] a = reversePrint0(list);
			System.out.println("调整完成");
			
			for (int i = 0; i < a.length; i++) {
				System.out.println(a[i]);
			}
		}
	 
	

}

```

