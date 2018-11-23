# 目录 #简单#Stack#
+ [20. 有效括号](#j1)
+ [155. 最小栈](#j2)
+ [225. 用队列实现栈](#j3)
+ [232. 用栈实现队列](#j4)




### <span id='j1'>20. 有效括号</span>
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。  

有效字符串需满足：  
* 左括号必须用相同类型的右括号闭合。  
* 左括号必须以正确的顺序闭合。  

注意空字符串可被认为是有效字符串。  

eg. 
```
输入: "()"
输出: true

输入: "()[]{}"
输出: true

输入: "(]"
输出: false

输入: "([)]"
输出: false

输入: "{[]}"
输出: true

```

```java
class Solution {
    private HashMap<Character, Character> mappings;
    
    public Solution(){
        this.mappings = new HashMap<Character, Character>();
        this.mappings.put(')', '(');
        this.mappings.put('}', '{');
        this.mappings.put(']', '[');
    }
    
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        
        for(int i = 0; i < s.length(); i++){
            char c = s.charAt(i);
            
            if(this.mappings.containsKey(c)){
                char topElement = stack.empty() ? '#' : stack.pop();
                
                if(topElement != this.mappings.get(c)){
                    return false;
                }
            } else {
                stack.push(c);
            }
        }
        return stack.isEmpty();
    }
}
```



### <span id='j2'>155. 最小栈</span>
设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。  

* push(x) -- 将元素 x 推入栈中。  
* pop() -- 删除栈顶的元素。  
* top() -- 获取栈顶元素。  
* getMin() -- 检索栈中的最小元素。   

eg.  
```java
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```

```java
class MinStack {

    Stack<Integer>stack=new Stack<Integer>();
    Stack<Integer>minstack=new Stack<Integer>();
    
    /** initialize your data structure here. */
    public MinStack() {             
    }
    
    public void push(int x) {
        if(minstack.isEmpty()||x<minstack.peek())
            minstack.push(x);
        else
            minstack.push(minstack.peek());
        stack.push(x);
    }
    
    public void pop() {
        minstack.pop();
        stack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return minstack.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```



### <span id='j3'>225. 用队列实现栈</span>
使用队列实现栈的下列操作：  

* push(x) -- 元素 x 入栈  
* pop() -- 移除栈顶元素  
* top() -- 获取栈顶元素  
* empty() -- 返回栈是否为空  

注意:  
你只能使用队列的基本操作-- 也就是 push to back, peek/pop from front, size, 和 is empty 这些操作是合法的。  
你所使用的语言也许不支持队列。 你可以使用 list 或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。  
你可以假设所有操作都是有效的（例如, 对一个空的栈不会调用 pop 或者 top 操作）。  

```java
class MyStack {
    
    List<Integer> list = new ArrayList<Integer>();

    /** Initialize your data structure here. */
    public MyStack() {
        
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        list.add(x);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        if(list.isEmpty()) return -1;
        return list.remove(list.size()-1);        
    }
    
    /** Get the top element. */
    public int top() {
        if(list.isEmpty()) return -1;
        return list.get(list.size()-1);
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return list.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```



### <span id='j4'>232. 用栈实现队列</span>
使用栈实现队列的下列操作：  

* push(x) -- 将一个元素放入队列的尾部。
* pop() -- 从队列首部移除元素。
* peek() -- 返回队列首部的元素。
* empty() -- 返回队列是否为空。
示例:  

```java
MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // 返回 1
queue.pop();   // 返回 1
queue.empty(); // 返回 false
```

说明:  

你只能使用标准的栈操作 -- 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。  
你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。  
假设所有操作都是有效的 （例如，一个空的队列不会调用 pop 或者 peek 操作）。  

```java
class MyQueue {
    
    Stack<Integer> s = new Stack<Integer>();
    Stack<Integer> sQueue = new Stack<Integer>();

    
    /** Initialize your data structure here. */
    public MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        while(!sQueue.isEmpty())  s.push(sQueue.pop());
        sQueue.push(x);
        while(!s.isEmpty())  sQueue.push(s.pop());
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if(sQueue.isEmpty()) return -1;
        return sQueue.pop();
    }
    
    /** Get the front element. */
    public int peek() {
        if(sQueue.isEmpty()) return -1;
        return sQueue.peek();
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return sQueue.isEmpty();
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```











