\> Problem: [剑指 Offer 30. 包含min函数的栈](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/description/)

[TOC]

# 剑指 Offer 30. 包含min函数的栈

### 思路

> 定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

> 解题思路

> 1. 第一种方法是使用两个栈来实现，用一个栈去存放对应的数据，用另一个栈去存放当前的最小值，在调用min()函数的时候，直接返回最小栈的数据即可
>    1. 题解动画详解 [剑指 Offer 30. 包含min函数的栈 - 力扣（LeetCode）](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/solutions/133760/mian-shi-ti-30-bao-han-minhan-shu-de-zhan-fu-zhu-z/)
> 2. 第二种方法是使用一个栈和一个最小值变量，用变量存放着最小值，用栈存放着当前插入数据与最小值的差值，在弹出数据的时候经过处理返回栈内的元素，当获取最小值的时候，直接返回单独的最小值变量







###  解题方法1

> 解题方法

> 1. 这里需要在pop和push的时候做特殊的处理，在push的时候，如果最小栈中没有元素，说明两个栈都是插入的第一个元素，所以两个栈中都要存放当前插入的x,如果在push的时候，新插入的数据值**小于等于**minStack栈顶的元素时候，需要在minStack中也插入当前值，表明这是最小值
>    1. 因为一开始只写了< 没有写等于号，对于重复的数据没有插入到minStack中导致在最后调用min()函数的时候导致栈空异常了
> 2. 在两个栈的时候，pop的时候，如果弹出的元素是minStack的栈顶元素 说明弹出的元素是当前的最小值，所以需要将minStack的栈顶元素弹出

####  复杂度

##### 时间复杂度: 

> 时间复杂度： $O(n)$
>

##### 空间复杂度: 

> 空间复杂度： $O(n)$

###  Code（自己写的）

```Java
class MinStack {

    Stack<Integer> stack ;
    Stack<Integer> minStack;
    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }
    
    public void push(int x) {
        if(stack.isEmpty()){
            stack.push(x);
            minStack.push(x);
        }else{
            stack.push(x);
        }
        if(x <= minStack.peek()){// 这里不能只在小于的时候加入到min栈，需要设定<=
        // 因为题目中没有说明不插入重复的数据，一开始在提交的时候，因为重复数据提交不通过
            minStack.push(x);
        }


    }
    
    public void pop() {
        int temp = stack.pop();
        if(temp == minStack.peek()){
            minStack.pop();
        }
    }
    
    public int top() {
        return stack.peek();

    }
    
    public int min() {
        return minStack.peek();
    }
}
```

###  Code（标准简化的）

```Java
class MinStack {
    Stack<Integer> A, B;
    public MinStack() {
        A = new Stack<>();
        B = new Stack<>();
    }
    public void push(int x) {
        A.add(x);
        if(B.empty() || B.peek() >= x)
            B.add(x);
    }
    public void pop() {
        if(A.pop().equals(B.peek()))
            B.pop();
    }
    public int top() {
        return A.peek();
    }
    public int min() {
        return B.peek();
    }
}

作者：Krahets
链接：https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/solutions/133760/mian-shi-ti-30-bao-han-minhan-shu-de-zhan-fu-zhu-z/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

### 帅地版本

> 帅地版本在设定的时候，因为Integer的范围是（-127——127） 所以使用intValue()函数进行下处理

```java


class MinStack {
    Stack<Integer> stack1;
    Stack<Integer> stack2;

    /** initialize your data structure here. */
    public MinStack() {
        this.stack1 = new Stack();
        this.stack2 = new Stack();
    }

    public void push(int x) {
        stack1.push(x);
        if(stack2.isEmpty() || x <= stack2.peek().intValue()){
            stack2.push(x);
        }
    }

    public void pop() {
        if(!stack1.isEmpty()){
            //Integer, 数值 > 127 I
            if(stack1.peek().intValue() == stack2.peek().intValue()){
                stack2.pop();
            }
            stack1.pop();
        }
    }

    public int top() {
        return stack1.peek();

    }

    public int min() {
        return stack2.peek();
    }
}
```







###  解题方法2**（待补充）**

> 解题方法

> 1. 这里需要在pop和push的时候做特殊的处理，在push的时候，如果最小栈中没有元素，说明两个栈都是插入的第一个元素，所以两个栈中都要存放当前插入的x,如果在push的时候，新插入的数据值**小于等于**minStack栈顶的元素时候，需要在minStack中也插入当前值，表明这是最小值
>    1. 因为一开始只写了< 没有写等于号，对于重复的数据没有插入到minStack中导致在最后调用min()函数的时候导致栈空异常了
> 2. 在两个栈的时候，pop的时候，如果弹出的元素是minStack的栈顶元素 说明弹出的元素是当前的最小值，所以需要将minStack的栈顶元素弹出

####  复杂度

##### 时间复杂度: 

> 时间复杂度： $O(n)$



##### 空间复杂度: 

> 空间复杂度： $O(n)$



###  Code

```Java

```

