\>Problem: [剑指 Offer 35. 复杂链表的复制](https://leetcode.cn/problems/fu-za-lian-biao-de-fu-zhi-lcof/description/)

[TOC]



### 思路

> 解题思路
>
> 这里因为有一个random指针指向，所以在复制的时候，需要复制random指针的前向节点和random指向的节点 ，所以不能像单链表复制那样，直接从头到尾进行复制；
>
> 1. 这里对原链表先进行扩充，让链表从A->B->C 变成A->A1->B->B1->C->C1  其中X1 表示对原数据的复制
> 2. 复制原来链表中的random节点，使得原链表中的random节点复制到新复制的X1节点上
> 3. 在将复制好的链表进行拆分，变成新的复制成品和原链表两个链表并返回新链表地址   A->A1->B->B1->C->C1 变成 A->B->C  A1->B1->C1 



> 详细思路 见这个链接里边的第二种方法
>
> [138. 复制带随机指针的链表 - 力扣（LeetCode）](https://leetcode.cn/problems/copy-list-with-random-pointer/solutions/2361362/138-fu-zhi-dai-sui-ji-zhi-zhen-de-lian-b-6jeo/)





> ==还有一种方法使用哈希表进行实现 这里没看==

###  解题方法

> 解题方法

> 1. 先复制链表【循环时逐个改变原链表节点的指针使其指向新建的节点并改变新建节点的next指向原节点的next使其连贯，直至复制到链表为空】
>
> 2. 设定新复制的节点的random节点，random节点应该是原链表节点的random指向的节点的next，因为新复制的节点在原链表节点的后一个代码实现的话是 cur.next.random = cur.ramdom.next
>
> 3. 拆分链表，使得  A->A1->B->B1->C->C1 变成 A->B->C  A1->B1->C1  新建两个头指针指向两个拆分好的链表，返回新的头指针
>
>    

###  复杂度

#### 时间复杂度: 

> 时间复杂度： $O(n)$
>
> m 和 n 分别是链表的长度



#### 空间复杂度: 

> 空间复杂度： $O(n)$

###  Code

```Java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    public Node copyRandomList(Node head) {

        

        if(head==null){
            return null;
        }

        // 先复制链表
        // 让链表从A->B->C 变成A->A1->B->B1->C->C1 //这里是对数据对复制， 然后在进行拆分

        // 先保存当前节点的next，再在next前边增加一个新的节点并且赋值为cur.val
        Node cur = head;
        while(cur != null){
            Node next = cur.next;
            cur.next = new Node(cur.val);//设定val值
            cur.next.next = next;       // 设定next值
            cur= next;					//cur后移，移动到原链表的下一个节点上继续进行复制
        }

        //保存完成原来的节点之后，修改新复制数据的random值，让他指向正确的数据
        // 这里要根据原来数据的random设定新的复制出的数据的random
        // A->A1->B->B1->C->C1  新复制的数据的random =当前指针的random指向的数据的next
        // 【因为新插入的数据  在原来数据的后边，所以要加一个next指向】
        cur = head;
        while(cur!= null){
            // cur.next.random = cur.random.next;//这里因为题目中提到可能为null
            //不能按照上边的写法，应该重写一下
            Node newNode = cur.next;
            newNode.random = cur.random == null ? null:cur.random.next;
            cur = cur.next.next; 
        }

        // 链表拆分，将一个链表拆分成两个分离的链表
        // A->A1->B->B1->C->C1 变成 A->B->C  A1->B1->C1 
        // 注意这里在更改的时候,已经改变了cur.next  一定要注意这一点
        
        Node headNew = head.next;// 指向新复制的链表的头结点也就是A1
        cur  =head;// 用来改变旧链表的next指向
        Node curNew = headNew;// 用来改变新链表的节点的next
        while(cur!=null){
            cur.next = cur.next.next;// 这里cur.next 已经从A1指向 B
            cur = cur.next;// 直接让cur 再从B继续

            // curNew.next  = cur.next;
            // 这里cur 已经从A指向 B.直接让curNew指向B1即可【
            // 注意cur可能为null也就是cur已经指向了最有一个节点,但是新链表还没更改,所以要单独设定】
            curNew.next = cur ==null? null:cur.next;
            curNew =curNew.next;
        }
        return headNew;

    }
        
}
```

