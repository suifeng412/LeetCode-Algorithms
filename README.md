# 目录 #简单#Stack#
+ [20. 有效括号](#j1)
+ [155. 最小栈](#j2)
+ [225. 用队列实现栈](#j3)
+ [232. 用栈实现队列](#j4)
+ [496. 下一个更大的元素](#j5)
+ [682. 棒球比赛](#j6)
+ [844. 比较含退格的字符串](#j7)



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


### <span id='j5'>496. 下一个更大的元素</span>
给定两个没有重复元素的数组 nums1 和 nums2 ，其中nums1 是 nums2 的子集。找到 nums1 中每个元素在 nums2 中的下一个比其大的值。  

nums1 中数字 x 的下一个更大元素是指 x 在 nums2 中对应位置的右边的第一个比 x 大的元素。如果不存在，对应位置输出-1。  

实例1:  
```
输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
输出: [-1,3,-1]
解释:
    对于num1中的数字4，你无法在第二个数组中找到下一个更大的数字，因此输出 -1。
    对于num1中的数字1，第二个数组中数字1右边的下一个较大数字是 3。
    对于num1中的数字2，第二个数组中没有下一个更大的数字，因此输出 -1。
```

实例2：  
```
输入: nums1 = [2,4], nums2 = [1,2,3,4].
输出: [3,-1]
解释:
    对于num1中的数字2，第二个数组中的下一个较大数字是3。
    对于num1中的数字4，第二个数组中没有下一个更大的数字，因此输出 -1。
```

注意:  
nums1和nums2中所有元素是唯一的。  
nums1和nums2 的数组大小都不超过1000。  

解决思路：  
通过Stack、HashMap解决  
1、先遍历大数组nums2，首先将第一个元素入栈；  
2、继续遍历，当当前元素小于栈顶元素时，继续将它入栈；当当前元素大于栈顶元素时，栈顶元素出栈，此时应将该出栈的元素与当前元素形成key-value键值对，存入HashMap中；  
3、当遍历完nums2后，得到nums2中元素所对应的下一个更大元素的hash表；  
4、遍历nums1的元素在hashMap中去查找‘下一个更大元素’，当找不到时则为-1。  

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Stack<Integer> stack = new Stack<Integer>();
        HashMap<Integer, Integer> hasMap = new HashMap<Integer, Integer>();
        
        int[] result = new int[nums1.length];
        
        for(int num : nums2) {
            while(!stack.isEmpty() && stack.peek()<num){
                hasMap.put(stack.pop(), num);
            }
            stack.push(num);
        }
        
        for(int i = 0; i < nums1.length; i++) result[i] = hasMap.getOrDefault(nums1[i], -1);
            
        return result;
    }
}
```


### <span id='j6'>682. 棒球比赛</span>
你现在是棒球比赛记录员。  
给定一个字符串列表，每个字符串可以是以下四种类型之一：  
1.整数（一轮的得分）：直接表示您在本轮中获得的积分数。  
2. "+"（一轮的得分）：表示本轮获得的得分是前两轮有效 回合得分的总和。  
3. "D"（一轮的得分）：表示本轮获得的得分是前一轮有效 回合得分的两倍。  
4. "C"（一个操作，这不是一个回合的分数）：表示您获得的最后一个有效 回合的分数是无效的，应该被移除。  

每一轮的操作都是永久性的，可能会对前一轮和后一轮产生影响。  
你需要返回你在所有回合中得分的总和。  

示例 1:  
```
输入: ["5","2","C","D","+"]
输出: 30
解释: 
第1轮：你可以得到5分。总和是：5。
第2轮：你可以得到2分。总和是：7。
操作1：第2轮的数据无效。总和是：5。
第3轮：你可以得到10分（第2轮的数据已被删除）。总数是：15。
第4轮：你可以得到5 + 10 = 15分。总数是：30。
```

示例 2:  
```
输入: ["5","-2","4","C","D","9","+","+"]
输出: 27
解释: 
第1轮：你可以得到5分。总和是：5。
第2轮：你可以得到-2分。总数是：3。
第3轮：你可以得到4分。总和是：7。
操作1：第3轮的数据无效。总数是：3。
第4轮：你可以得到-4分（第三轮的数据已被删除）。总和是：-1。
第5轮：你可以得到9分。总数是：8。
第6轮：你可以得到-4 + 9 = 5分。总数是13。
第7轮：你可以得到9 + 5 = 14分。总数是27。
```

注意：
* 输入列表的大小将介于1和1000之间。
* 列表中的每个整数都将介于-30000和30000之间。

```java
class Solution {
    public int calPoints(String[] ops) {
        Stack<Integer> stack = new Stack();

        for(String op : ops) {
            if (op.equals("+")) {
                int top = stack.pop();
                int newtop = top + stack.peek();
                stack.push(top);
                stack.push(newtop);
            } else if (op.equals("C")) {
                stack.pop();
            } else if (op.equals("D")) {
                stack.push(2 * stack.peek());
            } else {
                stack.push(Integer.valueOf(op));
            }
        }

        int ans = 0;
        for(int score : stack) ans += score;
        return ans;
    }
}
```



### <span id='j7'>844. 比较含退格的字符串</span>
给定 S 和 T 两个字符串，当它们分别被输入到空白的文本编辑器后，判断二者是否相等，并返回结果。 # 代表退格字符。   

示例 1：  
```
输入：S = "ab#c", T = "ad#c"
输出：true
解释：S 和 T 都会变成 “ac”。
``` 
示例 2：  
```
输入：S = "ab##", T = "c#d#"
输出：true
解释：S 和 T 都会变成 “”。
```
示例 3：  
```
输入：S = "a##c", T = "#a#c"
输出：true
解释：S 和 T 都会变成 “c”。
```
示例 4：   
```
输入：S = "a#c", T = "b"
输出：false
解释：S 会变成 “c”，但 T 仍然是 “b”。
```

提示：  
1 <= S.length <= 200  
1 <= T.length <= 200  
S 和 T 只含有小写字母以及字符 '#'。  

```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        Stack<Character> ss = new Stack<Character>();
        Stack<Character> ts = new Stack<Character>();
        
        for(int i = 0; i < S.length(); i++) {
            if(S.charAt(i) != '#')
                ss.push(S.charAt(i));      
            else if(!ss.isEmpty())
                  ss.pop(); 
        }
        
        for(int i = 0; i < T.length(); i++){
            if(T.charAt(i) != '#')
                ts.push(T.charAt(i)); 
            else if(!ts.isEmpty())
                ts.pop();
        }
        
        return ss.equals(ts);
    }
}
```








