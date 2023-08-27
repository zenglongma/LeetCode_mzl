\> Problem: [剑指 Offer 09. 用两个栈实现队列](https://leetcode.cn/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/description/)

[TOC]



### 思路

> 解题思路

> 使用两个栈实现队列的两个函数，模拟在队列尾部中插入新元素，和在队列头部弹出元素的过程

###  解题方法

> 解题方法

> 使用两个栈去实现一个队列，一个栈用于存放新插入队列的数据，一个栈用于出队列的数据
> 当插入队列的时候，将数据存放到入栈中，出队列时候，先从出栈中取出元素，如果出栈为空，
> 则将入队列中的数据全部放入到出栈并输出栈顶元素

###  复杂度

#### 时间复杂度: 

> 时间复杂度： $O(n)$
>

#### 空间复杂度: 

> 空间复杂度： $O(n)$



###  Code

```Java

class CQueue {
/**
使用两个栈去实现一个队列，一个栈用于存放新插入队列的数据，一个栈用于出队列的数据
当插入队列的时候，将数据存放到入栈中，出队列时候，先从出栈中取出元素，如果出栈为空，
则将入队列中的数据全部放入到出栈并输出栈顶元素
 */

    Stack<Integer> inStack;
    Stack<Integer> outStack;
    public CQueue() {
        inStack = new Stack<>();
        outStack = new Stack<>();
    }



    
    public void appendTail(int value) {// 在队列尾部插入数据
        inStack.push(value);// 直接在入栈中插入数据即可
    }
    
    public int deleteHead() {// 出队列
        if(!outStack.isEmpty()){// 出栈不为空
            return outStack.pop();
        }
        if(!inStack.isEmpty()){// 先保证入栈不为空
            while(!inStack.isEmpty()){//将入栈内的数据全部压入到出栈中
            outStack.push(inStack.pop());
            }
        return outStack.pop();
        }
        return -1; //两个栈都是空，则返回-1
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```

