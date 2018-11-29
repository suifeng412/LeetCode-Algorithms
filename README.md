# 目录 
## 简单#Stack#
+ [20. 有效括号](#j1)
+ [155. 最小栈](#j2)
+ [225. 用队列实现栈](#j3)
+ [232. 用栈实现队列](#j4)
+ [496. 下一个更大的元素](#j5)
+ [682. 棒球比赛](#j6)
+ [844. 比较含退格的字符串](#j7)

## 简单#Heap#
+ [703. 数据流中的第k大元素](#j8)
+ [743. 网络延迟时间](#j9)

## 简单#Greedy#
+ [122. 买卖股票的最佳时机](#j10)
+ [455. 分发饼干](#j11)
+ [860. 柠檬水找零](#j12)
+ [874. 模拟行走机器人](#j13)
+ [944. 删除列以使之有序](#j14)

## 简单#Array#
+ [1. 两数之和](#j15)
+ [26. 删除排序数组中的重复项](#j16)
+ [27. 移除元素](#j17)
+ [35. 搜索插入位置](#j18)




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



### <span id='j8'>703. 数据流中的第k大元素</span>
设计一个找到数据流中第K大元素的类（class）。注意是排序后的第K大元素，不是第K个不同的元素。  

你的 KthLargest 类需要一个同时接收整数 k 和整数数组nums 的构造器，它包含数据流中的初始元素。每次调用 KthLargest.add，返回当前数据流中第K大的元素。   

示例:  
```
int k = 3;
int[] arr = [4,5,8,2];
KthLargest kthLargest = new KthLargest(3, arr);
kthLargest.add(3);   // returns 4
kthLargest.add(5);   // returns 5
kthLargest.add(10);  // returns 5
kthLargest.add(9);   // returns 8
kthLargest.add(4);   // returns 8
```

说明:   
你可以假设 nums 的长度≥ k-1 且k ≥ 1。 

```java
class KthLargest {
  private final int[] heap;
  private final int k;
  private int size;

  public KthLargest(int k, int[] nums) {
    this.k = k;
    this.heap = new int[k + 1];
    for (int n : nums) add(n);
  }

  public int add(int val) {
    if (size < k) {
      // Build a min heap from the first k elements.
      heap[++size] = val;
      // Promote val to the top.
      for (int i = size; i > 1 && heap[i] < heap[i >>> 1];) swap(i, i >>>= 1);
    } else if (val > heap[1]) {
      // If val is greater than the minimum then it replaces the minimum.
      // Otherwise it's ignored.
      heap[1] = val;
      // Move val to the bottom.
      sink();
    }
    return heap[1];
  }

  private void sink() {
    int i = 1;
    while (i << 1 <= size) {
      // 2i and 2i+1 are the children of i.
      int j = i << 1;
      // If 2i+1 exists, choose the smallest of 2i and 2i+1.
      if (j < size && heap[j + 1] < heap[j]) j++;
      // If there are no children less than i then we're done.
      if (heap[i] <= heap[j]) break;
      // Otherwise swap i and the smallest of its children.
      swap(i, i = j);
    }
  }

  private void swap(int i, int j) {
    int t = heap[i];
    heap[i] = heap[j];
    heap[j] = t;
  }
}
```



### <span id='j9'>743. 网络延迟时间</span>
有 N 个网络节点，标记为 1 到 N。  

给定一个列表 times，表示信号经过有向边的传递时间。 times[i] = (u, v, w)，其中 u 是源节点，v 是目标节点， w 是一个信号从源节点传递到目标节点的时间。  

现在，我们向当前的节点 K 发送了一个信号。需要多久才能使所有节点都收到信号？如果不能使所有节点收到信号，返回 -1。  

注意:  
N 的范围在 [1, 100] 之间。  
K 的范围在 [1, N] 之间。  
times 的长度在 [1, 6000] 之间。   
所有的边 times[i] = (u, v, w) 都有 1 <= u, v <= N 且 1 <= w <= 100。  


迪杰克斯特拉算法Dijkstra Algorithm   
https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm#Using_a_priority_queue
```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        //graph存储图,数组第一个元素为终点，第二个元素为传播时间
        Map<Integer, List<int[]>> graph = new HashMap();
        for (int[] edge: times) {
            if (!graph.containsKey(edge[0]))    graph.put(edge[0], new ArrayList());
            graph.get(edge[0]).add(new int[]{edge[1], edge[2]});
        }
        //优先级队列，数组第一个元素为到该节点累计时间，第二个元素为节点号
        PriorityQueue<int[]> heap = new PriorityQueue<int[]>((info1, info2) -> info1[0] - info2[0]);
        heap.offer(new int[]{0, K});

        Map<Integer, Integer> dist = new HashMap();

        while (!heap.isEmpty()) {
            int[] info = heap.poll();
            int d = info[0], node = info[1];
            //如果dist包含该节点，说明已经获得了该节点的最短距离
            if (dist.containsKey(node)) continue;
            dist.put(node, d);
            if (graph.containsKey(node))
                for (int[] edge: graph.get(node)) {
                    int nei = edge[0], d2 = edge[1];
                    if (!dist.containsKey(nei))  heap.offer(new int[]{d + d2, nei});
                }
        }

        if (dist.size() != N) return -1;

        int ans = 0;
        for (int cand: dist.values())   ans = Math.max(ans, cand);

        return ans;
    }
}
```



### <span id='j10'>122. 买卖股票的最佳时机</span>
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。  

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。  

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。  

示例 1:  
```
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
```
示例 2:  
```
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```
示例 3:  
```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

```java
# 连续的峰和谷
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length==0)
            return 0;
        
        int i = 0;
        int valley = prices[0];
        int peak = prices[0];
        int maxprofit = 0;
        while (i < prices.length - 1) {
            while (i < prices.length - 1 && prices[i] >= prices[i + 1])
                i++;
            valley = prices[i];
            while (i < prices.length - 1 && prices[i] <= prices[i + 1])
                i++;
            peak = prices[i];
            maxprofit += peak - valley;
        }
        return maxprofit;
    }
}


class Solution {
    public int maxProfit(int[] prices) {
        int maxprofit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1])
                maxprofit += prices[i] - prices[i - 1];
        }
        return maxprofit;
    }
}
```




### <span id='j11'>455. 分发饼干</span>
假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。对每个孩子 i ，都有一个胃口值 gi ，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j ，都有一个尺寸 sj 。如果 sj >= gi ，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。  

注意：
你可以假设胃口值为正。  
一个小朋友最多只能拥有一块饼干。  

示例 1:  
```
输入: [1,2,3], [1,1]

输出: 1

解释: 
你有三个孩子和两块小饼干，3个孩子的胃口值分别是：1,2,3。
虽然你有两块小饼干，由于他们的尺寸都是1，你只能让胃口值是1的孩子满足。
所以你应该输出1。
```
示例 2:  
```
输入: [1,2], [1,2,3]

输出: 2

解释: 
你有两个孩子和三块小饼干，2个孩子的胃口值分别是1,2。
你拥有的饼干数量和尺寸都足以让所有孩子满足。
所以你应该输出2.
```

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int c=0;
        for(int i=0,j=0;j<s.length && i<g.length;j++){
            if(s[j]>=g[i]){
                c++;
            i++;
        }
    }

    return c;
    
    }
}
```



### <span id='j12'>860. 柠檬水找零</span>
在柠檬水摊上，每一杯柠檬水的售价为 5 美元。  
顾客排队购买你的产品，（按账单 bills 支付的顺序）一次购买一杯。  
每位顾客只买一杯柠檬水，然后向你付 5 美元、10 美元或 20 美元。你必须给每个顾客正确找零，也就是说净交易是每位顾客向你支付 5 美元。  

注意，一开始你手头没有任何零钱。  
如果你能给每位顾客正确找零，返回 true ，否则返回 false 。  

示例 1：  
```
输入：[5,5,5,10,20]
输出：true
解释：
前 3 位顾客那里，我们按顺序收取 3 张 5 美元的钞票。
第 4 位顾客那里，我们收取一张 10 美元的钞票，并返还 5 美元。
第 5 位顾客那里，我们找还一张 10 美元的钞票和一张 5 美元的钞票。
由于所有客户都得到了正确的找零，所以我们输出 true。
```
示例 2：  
```
输入：[5,5,10]
输出：true
```
示例 3：
```
输入：[10,10]
输出：false
```
示例 4：
```
输入：[5,5,10,10,20]
输出：false
解释：
前 2 位顾客那里，我们按顺序收取 2 张 5 美元的钞票。
对于接下来的 2 位顾客，我们收取一张 10 美元的钞票，然后返还 5 美元。
对于最后一位顾客，我们无法退回 15 美元，因为我们现在只有两张 10 美元的钞票。
由于不是每位顾客都得到了正确的找零，所以答案是 false。
```
提示：  
0 <= bills.length <= 10000  
bills[i] 不是 5 就是 10 或是 20  

```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int five = 0, ten = 0;
        for (int bill: bills) {
            if (bill == 5)
                five++;
            else if (bill == 10) {
                if (five == 0) return false;
                five--;
                ten++;
            } else {
                if (five > 0 && ten > 0) {
                    five--;
                    ten--;
                } else if (five >= 3) {
                    five -= 3;
                } else {
                    return false;
                }
            }
        }

        return true;
    }
}
``` 



### <span id='j13'>874. 模拟行走机器人</span>
机器人在一个无限大小的网格上行走，从点 (0, 0) 处开始出发，面向北方。该机器人可以接收以下三种类型的命令：  

-2：向左转 90 度  
-1：向右转 90 度  
1 <= x <= 9：向前移动 x 个单位长度  
在网格上有一些格子被视为障碍物。  

第 i 个障碍物位于网格点  (obstacles[i][0], obstacles[i][1])  

如果机器人试图走到障碍物上方，那么它将停留在障碍物的前一个网格方块上，但仍然可以继续该路线的其余部分。  

返回从原点到机器人的最大欧式距离的平方。  

示例 1：  
```
输入: commands = [4,-1,3], obstacles = []
输出: 25
解释: 机器人将会到达 (3, 4)
```
示例 2：  
```
输入: commands = [4,-1,4,-2,4], obstacles = [[2,4]]
输出: 65
解释: 机器人在左转走到 (1, 8) 之前将被困在 (1, 4) 处
```
提示：  
```
0 <= commands.length <= 10000  
0 <= obstacles.length <= 10000  
-30000 <= obstacle[i][0] <= 30000  
-30000 <= obstacle[i][1] <= 30000  
答案保证小于 2 ^ 31  
```

```java
class Solution {
    public int robotSim(int[] commands, int[][] obstacles) {
        int[] dx = new int[]{0, 1, 0, -1};
        int[] dy = new int[]{1, 0, -1, 0};
        int x = 0, y = 0, di = 0;

        // Encode obstacles (x, y) as (x+30000) * (2^16) + (y+30000)
        Set<Long> obstacleSet = new HashSet();
        for (int[] obstacle: obstacles) {
            long ox = (long) obstacle[0] + 30000;
            long oy = (long) obstacle[1] + 30000;
            obstacleSet.add((ox << 16) + oy);
        }

        int ans = 0;
        for (int cmd: commands) {
            if (cmd == -2)  //left
                di = (di + 3) % 4;
            else if (cmd == -1)  //right
                di = (di + 1) % 4;
            else {
                for (int k = 0; k < cmd; ++k) {
                    int nx = x + dx[di];
                    int ny = y + dy[di];
                    long code = (((long) nx + 30000) << 16) + ((long) ny + 30000);
                    if (!obstacleSet.contains(code)) {
                        x = nx;
                        y = ny;
                        ans = Math.max(ans, x*x + y*y);
                    }
                }
            }
        }

        return ans;
    }
}
```



### <span id='j14'>944. 删除列以使之有序</span>
给出由 N 个小写字母串组成的数组 A，所有小写字母串的长度都相同。  
现在，我们可以选择任何一组删除索引，对于每个字符串，我们将删除这些索引中的所有字符。  

举个例子，如果字符串为 "abcdef"，且删除索引是 {0, 2, 3}，那么删除之后的最终字符串为 "bef"。   
假设我们选择了一组删除索引 D，在执行删除操作之后，A 中剩余的每一列都是有序的。  
形式上，第 c 列为 [A[0][c], A[1][c], ..., A[A.length-1][c]]  
返回 D.length 的最小可能值。  

通俗的说就是A数组中有多少列是非升序的。  
示例 1：
```
输入：["cba","daf","ghi"]
输出：1
```
示例 2：
```
输入：["a","b"]
输出：0
```
示例 3：
```
输入：["zyx","wvu","tsr"]
输出：3
```
提示：  
* 1 <= A.length <= 100
* 1 <= A[i].length <= 1000

```java
class Solution {
    public int minDeletionSize(String[] A) {
        if(A == null || A.length == 0) return 0;
        //所有小写字母串的长度都相同
        int count = 0;
        for(int i = 0;i < A[0].length();i++){
            for(int j = 0;j < A.length - 1;j++){
                if(A[j].charAt(i) > A[j+1].charAt(i)){
                    count++;
                    break;
                } 
            }            
        }
        
        return  count;
    }
}
```



### <span id='j15'>1. 两数之和</span>
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的 两个整数。  
你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。  

示例:
```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
         }
          map.put(nums[i], i);
      }
    throw new IllegalArgumentException("No two sum solution");
    }
}
```



### <span id='j16'>26. 删除排序数组中的重复项</span>
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。  
不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。  

示例 1:  
```
给定数组 nums = [1,1,2], 
函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 
你不需要考虑数组中超出新长度后面的元素。
```
示例 2:
```
给定 nums = [0,0,1,1,1,2,2,3,3,4],
函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。
你不需要考虑数组中超出新长度后面的元素。
```
说明:  
为什么返回数值是整数，但输出的答案是数组呢?  
请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。  
你可以想象内部操作如下:  
```
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int num=0;
        for(int i=0; i<nums.length; i++){
            if(i==0 || nums[i] != nums[i-1])    
                nums[num++] = nums[i];
                
        }
        return num;
    }
}
```



### <span id='j17'>27. 移除元素</span>
给定一个数组 nums 和一个值 val，你需要原地移除所有数值等于 val 的元素，返回移除后数组的新长度。   
不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。  
元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。  

示例 1:  
```
给定 nums = [3,2,2,3], val = 3,
函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。
你不需要考虑数组中超出新长度后面的元素。
```
示例 2:
```
给定 nums = [0,1,2,2,3,0,4,2], val = 2,
函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。
注意这五个元素可为任意顺序。
你不需要考虑数组中超出新长度后面的元素。
```
说明:  
为什么返回数值是整数，但输出的答案是数组呢?
请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。
你可以想象内部操作如下:
```
// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
int len = removeElement(nums, val);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
```java
# 方法一
class Solution {
    public int removeElement(int[] nums, int val) {
        int len = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] != val)
                nums[len++] = nums[i];
        }
        return len;
    }
}

# 方法二
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        int len = nums.length;
        while(i < len){
            if(nums[i] == val)
                nums[i] = nums[--len];
            else
                i++;
        }
        return i;
    }
}

```



### <span id='j18'>35. 搜索插入位置</span>
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。  
你可以假设数组中无重复元素。  

示例 1:
```
输入: [1,3,5,6], 5
输出: 2
```
示例 2:
```
输入: [1,3,5,6], 2
输出: 1
```
示例 3:
```
输入: [1,3,5,6], 7
输出: 4
```
示例 4:
```
输入: [1,3,5,6], 0
输出: 0
```

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int i;
        for(i=0; i < nums.length; i++){
            if(nums[i] >= target)
                break;
        }
        return i;
    }
}
```





