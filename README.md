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
+ [53. 最大子序和](#j19)
+ [66. 加一](#j20)
+ [88. 合并两个有序数组](#j21)
+ [118. 杨辉三角](#j22)
+ [119. 杨辉三角 II](#j23)
+ [121. 买卖股票的最佳时机](#j24)
+ [167. 两数之和 II - 输入有序数组](#j25)
+ [169. 求众数](#j26)
+ [189. 旋转数组](#j27)
+ [217. 存在重复元素](#j28)
+ [219. 存在重复元素 II](#j29)
+ [268. 缺失数字](#j30)
+ [283. 移动零](#j31)
+ [414. 第三大的数](#j32)
+ [448. 找到所有数组中消失的数字](#j33)
+ [485. 最大连续1的个数](#j34)
+ [532. 数组中的K-diff数对](#j35)
+ [561. 数组拆分 I](#j36)
+ [566. 重塑矩阵](#j37)
+ [581. 最短无序连续子数组](#j38)
+ [605. 种花问题](#j39)
+ [628. 三个数的最大乘积](#j40)
+ [643. 子数组最大平均数 I](#j41)
+ [661. 图片平滑器](#j42)
+ [665. 非递减数列](#j43)
+ [674. 最长连续递增序列](#j44)
+ [697. 数组的度](#j45)
+ [717. 1比特与2比特字符](#j46)
+ [724. 寻找数组的中心索引](#j47)
+ [746. 使用最小花费爬楼梯](#j48)
+ [747. 至少是其他数字两倍的最大数](#j49)
+ [766. 托普利茨矩阵](#j50)
+ [830. 较大分组的位置](#j51)
+ [832. 翻转图像](#j52)
+ [840. 矩阵中的幻方](#j52)
+ [849. 到最近的人的最大距离](#j53)
+ [867. 转置矩阵](#j54)
+ [888. 公平的糖果交换](#j55)
+ [896. 单调数列](#j56)
+ [905. 按奇偶排序数组](#j57)
+ [914. 卡牌分组](#j58)
+ [922. 按奇偶排序数组 II](#j59)
+ [941. 有效的山脉数组](#j60)



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



### <span id='j19'>53. 最大子序和</span>
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。  

示例:
```
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```
进阶:  
如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。  

```
class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        int sum = 0;
        for (int num : nums) {
            if (sum > 0)
                sum += num;
            else
                sum = num;
            res = Math.max(res, sum);
        }
        return res;
    }
}
```



### <span id='j20'>66. 加一</span>
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。  
最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。  
你可以假设除了整数 0 之外，这个整数不会以零开头。  

示例 1:  
```
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。
```
示例 2:  
```
输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
```

```
class Solution {
    public int[] plusOne(int[] digits) {
        int len = digits.length;
        
        // 反向迭代
        for(int i = digits.length-1; i>=0; i--){
            if(digits[i]+1 == 10){       // 有进一就继续迭代
                digits[i] = 0;
            }else{                      // 否则退出循环
                digits[i]++;
                break;
            }  
        }
        
        
        if(len == 0){       // 空数组的时候
            return new int[]{1};
        }else if(digits[0] == 0){       // 最高位也进一的时候
            int res[] = new int[len+1];
            res[0] = 1;
            System.arraycopy(digits, 0, res, 1, len);
            return res;
        }
          
        return digits;
    }
}
```



### <span id='j21'>88. 合并两个有序数组</span>
给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。  
说明:  
初始化 nums1 和 nums2 的元素数量分别为 m 和 n。   
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。  
示例:
```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int j = 0;
        int i = 0;
        
        while( j < n  && i < m+n){
            if((int)nums1[i] > (int)nums2[j]){
                System.arraycopy(nums1, i, nums1, i+1, (n+m-i-1));
                nums1[i] = nums2[j];
                j++;
            }else if(nums1[i] <= nums2[j] && i-j==m && nums1[i]==0){
                System.arraycopy(nums2, j, nums1, i, n-j);
                break;
            }
            
            i++;
        }

    }
}
```


### <span id='j22'>118. 杨辉三角</span>
给定一个非负整数 numRows，生成杨辉三角的前 numRows 行  
在杨辉三角中，每个数是它左上方和右上方的数的和。  
示例:
```
输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> triangle = new ArrayList<List<Integer>>();

        if (numRows == 0) {
            return triangle;
        }

        triangle.add(new ArrayList<>());
        triangle.get(0).add(1);

        for (int rowNum = 1; rowNum < numRows; rowNum++) {
            List<Integer> row = new ArrayList<>();
            List<Integer> prevRow = triangle.get(rowNum-1);

            row.add(1);


            for (int j = 1; j < rowNum; j++) {
                row.add(prevRow.get(j-1) + prevRow.get(j));
            }

            row.add(1);

            triangle.add(row);
        }

        return triangle;
    }
}
```

### <span id='j23'>119. 杨辉三角 II</span>
给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。  
在杨辉三角中，每个数是它左上方和右上方的数的和。  
示例:
```
输入: 3
输出: [1,3,3,1]
```
进阶：  
你可以优化你的算法到 O(k) 空间复杂度吗？

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> list=new ArrayList<Integer>();

        for(int i=0;i<=rowIndex;i++){
            list.add(1);
            for(int j=i-1;j>=1;j--){
                list.set(j, list.get(j)+list.get(j-1) );
            }

        }
        return list;
    }
}
```

### <span id='j24'>121. 买卖股票的最佳时机</span>
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。  
如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。   
注意你不能在买入股票前卖出股票。  
示例 1:
```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```
示例 2:
```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

```java
# 方法一 暴力法
public class Solution {
    public int maxProfit(int prices[]) {
        int maxprofit = 0;
        for (int i = 0; i < prices.length - 1; i++) {
            for (int j = i + 1; j < prices.length; j++) {
                int profit = prices[j] - prices[i];
                if (profit > maxprofit)
                    maxprofit = profit;
            }
        }
        return maxprofit;
    }
}

# 方法二 一次遍历
public class Solution {
    public int maxProfit(int prices[]) {
        int minprice = Integer.MAX_VALUE;
        int maxprofit = 0;
        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < minprice)
                minprice = prices[i];
            else if (prices[i] - minprice > maxprofit)
                maxprofit = prices[i] - minprice;
        }
        return maxprofit;
    }
}
```



### <span id='j25'>167. 两数之和 II - 输入有序数组</span>
给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。  
函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。  

说明:  

返回的下标值（index1 和 index2）不是从零开始的。  
你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。  
示例:
```
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

```java
# 方法一  O(n)
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        HashMap<Integer, Integer> hashMap = new HashMap<Integer, Integer>();
        
        for(int i=0; i<numbers.length; i++){
            int num = target-numbers[i];
            if(hashMap.get(num) != null)
                return new int[]{hashMap.get(num), i+1};
            else
                hashMap.put(numbers[i], i+1);
        }
        return new int[]{};
    }
    
}

# 方法二 双指针 TODO
```



### <span id='j26'>169. 求众数</span>
给定一个大小为 n 的数组，找到其中的众数。众数是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。  
你可以假设数组是非空的，并且给定的数组总是存在众数。  

示例 1:
```
输入: [3,2,3]
输出: 3
```
示例 2:
```
输入: [2,2,1,1,1,2,2]
输出: 2
```

```java
# 摩尔投票法
class Solution {
    public int majorityElement(int[] nums) {
        int count = 1;
		int maj = nums[0];
		for (int i = 1; i < nums.length; i++) {
			if (maj == nums[i])
				count++;
			else {
				count--;
				if (count == 0) {
					maj = nums[i + 1];
				}
			}
		}
		return maj; 
    }
}
```



### <span id='j27'>189. 旋转数组</span>
给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。  
示例 1:
```
输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]
```

示例 2:
```
输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释: 
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]
```

说明:  
尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。  
要求使用空间复杂度为 O(1) 的原地算法。  

```java
# 方法一 暴力破解
public class Solution {
    public void rotate(int[] nums, int k) {
        int temp, previous;
        for (int i = 0; i < k; i++) {
            previous = nums[nums.length - 1];
            for (int j = 0; j < nums.length; j++) {
                temp = nums[j];
                nums[j] = previous;
                previous = temp;
            }
        }
    }
}

# 方法二 使用额外空间
public class Solution {
    public void rotate(int[] nums, int k) {
        int[] a = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            a[(i + k) % nums.length] = nums[i];
        }
        for (int i = 0; i < nums.length; i++) {
            nums[i] = a[i];
        }
    }
}

# 方法三 循环一个一个替换
public class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        int count = 0;
        for (int start = 0; count < nums.length; start++) {
            int current = start;
            int prev = nums[start];
            do {
                int next = (current + k) % nums.length;
                int temp = nums[next];
                nums[next] = prev;
                prev = temp;
                current = next;
                count++;
            } while (start != current);
        }
    }
}
```



### <span id='j28'>217. 存在重复元素</span>
给定一个整数数组，判断是否存在重复元素。  

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。  

示例 1:
```
输入: [1,2,3,1]
输出: true
```
示例 2:
```
输入: [1,2,3,4]
输出: false
```
示例 3:
```
输入: [1,1,1,3,3,4,3,2,4,2]
输出: true
```

```java
# 方法一
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 1; ++i) {
            if (nums[i] == nums[i + 1]) return true;
        }
        return false;
    }
}

# 方法二
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashMap<Integer, Integer> hashMap = new HashMap<Integer, Integer>();
        
        for(int i=0; i<nums.length; i++){
             if(hashMap.get(nums[i]) != null)
                return true;
            else
                hashMap.put(nums[i], i);
        }
        
        return false;
    }
}
```



### <span id='j29'>219. 存在重复元素 II</span>
给定一个整数数组和一个整数 k，判断数组中是否存在两个不同的索引 i 和 j，使得 nums [i] = nums [j]，并且 i 和 j 的差的绝对值最大为 k。  

示例 1:
```
输入: nums = [1,2,3,1], k = 3
输出: true
```
示例 2:
```
输入: nums = [1,0,1,1], k = 1
输出: true
```
示例 3:
```
输入: nums = [1,2,3,1,2,3], k = 2
输出: false
```

```java

class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        HashMap<Integer,Integer> hashMap = new HashMap<>();
        for(int i=0;i<nums.length;i++){
            if(hashMap.containsKey(nums[i])){
                int sub = i - hashMap.get(nums[i]);
                if(sub <= k)
                    return true;
                else
                    hashMap.put(nums[i],i);
            }
            else
                hashMap.put(nums[i],i);
        }
        return false;
    }
}
```


### <span id='j30'>268. 缺失数字</span>
给定一个包含 0, 1, 2, ..., n 中 n 个数的序列，找出 0 .. n 中没有出现在序列中的那个数。  

示例 1:
```
输入: [3,0,1]
输出: 2
```
示例 2:
```
输入: [9,6,4,2,3,5,7,0,1]
输出: 8
```

```java
class Solution {
    public int missingNumber(int[] nums) {
        int sum = 0;
        int len = nums.length;
        
        if(len%2 == 0)
            sum = (len*len+len)/2;
        else
            sum = len*(len+1)/2;
        
        
        for(int i=0; i<len; i++)
            sum -= nums[i];
        
        return sum;
    }
}
```



### <span id='j31'>283. 移动零</span>
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。  

示例:
```
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```
说明:  
必须在原数组上操作，不能拷贝额外的数组。  
尽量减少操作次数。  

```java
class Solution {
    public void moveZeroes(int[] nums) {
        
        int j = 0;
        int len = nums.length;
        
        for(int i=0; i<len; i++){
            if(nums[i] != 0){
                nums[j++] = nums[i];
            }
        }
        
        while(j < len)
        {
            nums[j++] = 0;
        }
        
    }
}
```



### <span id='j32'>414. 第三大的数</span>
给定一个非空数组，返回此数组中第三大的数。如果不存在，则返回数组中最大的数。要求算法时间复杂度必须是O(n)。  

示例 1:
```
输入: [3, 2, 1]
输出: 1
解释: 第三大的数是 1.
```
示例 2:
```
输入: [1, 2]
输出: 2
解释: 第三大的数不存在, 所以返回最大的数 2 .
```
示例 3:
```
输入: [2, 2, 3, 1]
输出: 1
解释: 注意，要求返回第三大的数，是指第三大且唯一出现的数。
```
存在两个值为2的数，它们都排第二。  

```java
class Solution {
    public int thirdMax(int[] nums) {
        Integer maxF = null;
        Integer maxS = null;
        Integer maxT = null;
 
        for( Integer i : nums){
            if (i.equals(maxF) || i.equals(maxT) || i.equals(maxS)){
                continue;
            }else if ( maxF == null || i > maxF ){
                maxT = maxS;
                maxS = maxF;
                maxF = i;
            }else if (maxS == null || i > maxS){
                maxT = maxS;
                maxS = i;
            }else if (maxT == null || i > maxT){
                maxT = i;
            }
 
        }
 
        return maxT == null ? maxF : maxT;
    }
}

```


### <span id='j33'>448. 找到所有数组中消失的数字</span>
给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。  
找到所有在 [1, n] 范围之间没有出现在数组中的数字。  

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。  

示例:
```
输入:
[4,3,2,7,8,2,3,1]
输出:
[5,6]
```

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> list = new ArrayList<Integer>();
        
        int len = nums.length;
        int[] nums2 = new int[len];
        
        for(int i=0; i<len; i++)
            nums2[nums[i]-1] = 1;
    
        for(int i=0; i<len; i++){
            if(nums2[i] != 1)
                list.add(i+1);
        }
        return list; 
    }
}
```



### <span id='j34'>485. 最大连续1的个数</span>
给定一个二进制数组， 计算其中最大连续1的个数。  

示例 1:
```
输入: [1,1,0,1,1,1]
输出: 3
解释: 开头的两位和最后的三位都是连续1，所以最大连续1的个数是 3.
```
注意：  
输入的数组只包含 0 和1。  
输入数组的长度是正整数，且不超过 10,000。  

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        
        int max = 0;
        int temp = 0;
        
        for(Integer i : nums){
            
            if(i == 0){
                max = max > temp ? max : temp;
                temp = 0;
            }else{
               temp++; 
            }
            
        }
        return max > temp ? max : temp;
    }
}
```






### <span id='j35'>532. 数组中的K-diff数对</span>
给定一个整数数组和一个整数 k, 你需要在数组里找到不同的 k-diff 数对。这里将 k-diff 数对定义为一个整数对 (i, j), 其中 i 和 j 都是数组中的数字，且两数之差的绝对值是 k.  

示例 1:
```
输入: [3, 1, 4, 1, 5], k = 2
输出: 2
解释: 数组中有两个 2-diff 数对, (1, 3) 和 (3, 5)。
尽管数组中有两个1，但我们只应返回不同的数对的数量。
```
示例 2:
```
输入:[1, 2, 3, 4, 5], k = 1
输出: 4
解释: 数组中有四个 1-diff 数对, (1, 2), (2, 3), (3, 4) 和 (4, 5)。
```
示例 3:
```
输入: [1, 3, 1, 5, 4], k = 0
输出: 1
解释: 数组中只有一个 0-diff 数对，(1, 1)。
```
注意:  
数对 (i, j) 和数对 (j, i) 被算作同一数对。  
数组的长度不超过10,000。  
所有输入的整数的范围在 [-1e7, 1e7]。  

```java
class Solution {
    public int findPairs(int[] nums, int k) {
        HashMap<Integer, Integer> hashMap = new HashMap<Integer, Integer>();
        int count = 0;
        
        for(Integer num : nums){
            if(k == 0 && hashMap.getOrDefault(num, 0)>0 && hashMap.get(num)<2){
                count ++;
                hashMap.put(num, 2);
            }else if(k == 0 && hashMap.getOrDefault(num, 0)>0){
                continue;
            }else{
                hashMap.put(num, 1);
            }
        }
        
        
        if(k > 0){
            for(Integer key:hashMap.keySet()){
                if(hashMap.getOrDefault(key+k, 0)>0){
                    count++;
                }     
            }
        }


        return count;
    }
}
```



### <span id='j36'>561. 数组拆分 I</span>
给定长度为 2n 的数组, 你的任务是将这些数分成 n 对, 例如 (a1, b1), (a2, b2), ..., (an, bn) ，使得从1 到 n 的 min(ai, bi) 总和最大。  

示例 1:
```
输入: [1,4,3,2]
输出: 4
解释: n 等于 2, 最大总和为 4 = min(1, 2) + min(3, 4).
```
提示:  
n 是正整数,范围在 [1, 10000].  
数组中的元素范围在 [-10000, 10000].  

```java
public class Solution {

	public int arrayPairSum(int[] nums) {
		int[] exist = new int[20001];
		for (int i = 0; i < nums.length; i++) {
			exist[nums[i] + 10000]++;
		}
		int sum = 0;
		boolean odd = true;
		for (int i = 0; i < exist.length; i++) {
			while (exist[i] > 0) {
				if (odd) {
					sum += i - 10000;
				}
				odd = !odd;
				exist[i]--;
			}
		}
		return sum;
	}
	
}
```



### <span id='j37'>566. 重塑矩阵</span>
在MATLAB中，有一个非常有用的函数 reshape，它可以将一个矩阵重塑为另一个大小不同的新矩阵，但保留其原始数据。  
给出一个由二维数组表示的矩阵，以及两个正整数r和c，分别表示想要的重构的矩阵的行数和列数。  
重构后的矩阵需要将原始矩阵的所有元素以相同的行遍历顺序填充。  

如果具有给定参数的reshape操作是可行且合理的，则输出新的重塑矩阵；否则，输出原始矩阵。  

示例 1:
```
输入: 
nums = 
[[1,2],
 [3,4]]
r = 1, c = 4
输出: 
[[1,2,3,4]]
解释:
行遍历nums的结果是 [1,2,3,4]。新的矩阵是 1 * 4 矩阵, 用之前的元素值一行一行填充新矩阵。
```
示例 2:
```
输入: 
nums = 
[[1,2],
 [3,4]]
r = 2, c = 4
输出: 
[[1,2],
 [3,4]]
解释:
没有办法将 2 * 2 矩阵转化为 2 * 4 矩阵。 所以输出原矩阵。
```
注意：
给定矩阵的宽和高范围在 [1, 100]。  
给定的 r 和 c 都是正数。  

```java
class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        
        if(r*c == nums.length*nums[0].length){
            int[][] res = new int[r][c];
            
            int i = 0;
            int rr = 0;
            int cc = 0;

            while(i<nums.length){
                for(int j=0; j<nums[0].length; j++){
                    if(cc<c){
                       res[rr][cc++] = nums[i][j]; 
                    }else{
                        cc = 0;
                        res[++rr][cc++] = nums[i][j]; 
                    }
                }   
                i++;
            }
            return res;
        }else{
            return nums;
        }
         
    }
}
```



### <span id='j38'>581. 最短无序连续子数组</span>
给定一个整数数组，你需要寻找一个连续的子数组，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。  
你找到的子数组应是最短的，请输出它的长度。  

示例 1:
```
输入: [2, 6, 4, 8, 10, 9, 15]
输出: 5
解释: 你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
```
说明 :  
输入的数组长度范围在 [1, 10,000]。  
输入的数组可能包含重复元素 ，所以升序的意思是<=。  

```java
// 从右到左，维护更新min 和 beg；
// 从左到右，维护更新max 和 end。

class Solution 
{
    public int findUnsortedSubarray(int[] nums) 
    {
        int n = nums.length;
        int beg = -1;
        int end = -2; 
        
        int min = nums[n-1]; 
        int max = nums[0];   
        
        
        for(int i=0; i<n; i++)
        {
            max = Math.max(max, nums[i]);
            min = Math.min(min, nums[n-1-i]);
            
            if(nums[i] < max)
                end = i;
            if(nums[n-1-i] > min)
                beg = n-1-i;
        }
        
        return end - beg + 1; 
    }
}
```
   
   


### <span id='j39'>605. 种花问题</span>
假设你有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花卉不能种植在相邻的地块上，它们会争夺水源，两者都会死去。  
给定一个花坛（表示为一个数组包含0和1，其中0表示没种植花，1表示种植了花），和一个数 n 。能否在不打破种植规则的情况下种入 n 朵花？能则返回True，不能则返回False。  

示例 1:
```
输入: flowerbed = [1,0,0,0,1], n = 1
输出: True
```
示例 2:
```
输入: flowerbed = [1,0,0,0,1], n = 2
输出: False
```
注意:  
数组内已种好的花不会违反种植规则。  
输入的数组长度范围为 [1, 20000]。  
n 是非负整数，且不会超过输入数组的大小。  

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int len = flowerbed.length;      
        
        Boolean before;
        Boolean after;
        
        for(int i=0; i<len; i++){
            
            if(flowerbed[i] == 0){
                before = true;
                after = true;
                
                if(i+1 < len)
                    after = flowerbed[i+1] == 0 ? true : false; 
                if(i-1 >= 0)
                    before = flowerbed[i-1] == 0 ? true : false; 
            
                if(after && before){
                    n--;
                    flowerbed[i] = 1;
                }

            }

        }

        return n > 0 ? false : true;
        
        
    }
}
```

   
   
   
### <span id='j40'>628. 三个数的最大乘积  </span>
给定一个整型数组，在数组中找出由三个数组成的最大乘积，并输出这个乘积。  

示例 1:
```
输入: [1,2,3]
输出: 6
```
示例 2:
```
输入: [1,2,3,4]
输出: 24
```
注意:  
给定的整型数组长度范围是[3,104]，数组中所有的元素范围是[-1000, 1000]。  
输入的数组中任意三个数的乘积不会超出32位有符号整数的范围。  

```java
public class Solution {
    public int maximumProduct(int[] nums) {
        int min1 = Integer.MAX_VALUE, min2 = Integer.MAX_VALUE;
        int max1 = Integer.MIN_VALUE, max2 = Integer.MIN_VALUE, max3 = Integer.MIN_VALUE;
        for (int n: nums) {
            if (n <= min1) {
                min2 = min1;
                min1 = n;
            } else if (n <= min2) {    
                min2 = n;
            }
            if (n >= max1) {            
                max3 = max2;
                max2 = max1;
                max1 = n;
            } else if (n >= max2) {     
                max3 = max2;
                max2 = n;
            } else if (n >= max3) {     
                max3 = n;
            }
        }
        return Math.max(min1 * min2 * max1, max1 * max2 * max3);
    }
}
```



### <span id='j41'>643. 子数组最大平均数 I</span>
给定 n 个整数，找出平均数最大且长度为 k 的连续子数组，并输出该最大平均数。  

示例 1:
```
输入: [1,12,-5,-6,50,3], k = 4
输出: 12.75
解释: 最大平均数 (12-5-6+50)/4 = 51/4 = 12.75
```
注意:  
1 <= k <= n <= 30,000。  
所给数据范围 [-10,000，10,000]。    

```java
public class Solution {
    public double findMaxAverage(int[] nums, int k) {
        if (nums.length < 1 || nums == null) {
            return -1;
        }
        int sum = 0;
        int max = 0;
        for (int i = 0; i < k; i++) {
            sum += nums[i];// 先求前k个数的和，之后不断维护这个数组即可。
            max = sum;
        }
        for (int i = k; i < nums.length; i++) {
            sum += nums[i] - nums[i - k];
            if (sum > max) {
                max = sum;
            }
        }
        return max * 1.0 / k;
    }
}
```


### <span id='j42'>661. 图片平滑器</span>
包含整数的二维矩阵 M 表示一个图片的灰度。你需要设计一个平滑器来让每一个单元的灰度成为平均灰度 (向下舍入) ，平均灰度的计算是周围的8个单元和它本身的值求平均，如果周围的单元格不足八个，则尽可能多的利用它们。  

示例 1:
```
输入:
[[1,1,1],
 [1,0,1],
 [1,1,1]]
输出:
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]
解释:
对于点 (0,0), (0,2), (2,0), (2,2): 平均(3/4) = 平均(0.75) = 0
对于点 (0,1), (1,0), (1,2), (2,1): 平均(5/6) = 平均(0.83333333) = 0
对于点 (1,1): 平均(8/9) = 平均(0.88888889) = 0
```
注意:  
给定矩阵中的整数范围为 [0, 255]。  

```java
class Solution 
{
    public int[][] imageSmoother(int[][] M) 
    {
        int rows = M.length;
        int cols = M[0].length;
        int[][] res = new int[rows][cols];
        
        for(int i=0; i<rows; i++)
        {
            for(int j=0; j<cols; j++)
            {
                int sum = 0;
                int count = 0;
                // sum 3x3 area and take care of the boundary
                for(int x=Math.max(0,i-1); x<=Math.min(rows-1, i+1); x++)
                {
                    for(int y=Math.max(0, j-1); y<=Math.min(cols-1, j+1); y++)
                    {
                        sum += M[x][y]; // sum up cells value
                        count++; // count cells number
                    }
                }
                
                res[i][j] = sum / count; // get average value
            }
        }
        
        return res;
    }
}
```



### <span id='j43'>665. 非递减数列</span>
给定一个长度为 n 的整数数组，你的任务是判断在最多改变 1 个元素的情况下，该数组能否变成一个非递减数列。  
我们是这样定义一个非递减数列的： 对于数组中所有的 i (1 <= i < n)，满足 array[i] <= array[i + 1]。  

示例 1:  
```
输入: [4,2,3]
输出: True
解释: 你可以通过把第一个4变成1来使得它成为一个非递减数列。
```
示例 2:
```
输入: [4,2,1]
输出: False
解释: 你不能在只改变一个元素的情况下将其变为非递减数列。
```
说明:  n 的范围为 [1, 10,000]。

```java
class Solution {
    public boolean checkPossibility(int[] nums) {
        int count = 0;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < nums[i - 1]) {
                count++;
                if (count > 1) {
                    return false;
                }
                int privous = i > 1 ? nums[i - 2] : 0;
                int after = i < nums.length - 1 ? nums[i + 1] : 10000;
                if (nums[i - 1] > after && nums[i] < privous) {
                    return false;
                }
            }
        }
        return true;
    }
}
```


### <span id='j44'>674. 最长连续递增序列</span>
给定一个未经排序的整数数组，找到最长且连续的的递增序列。  

示例 1:
```
输入: [1,3,5,4,7]
输出: 3
解释: 最长连续递增序列是 [1,3,5], 长度为3。
尽管 [1,3,5,7] 也是升序的子序列, 但它不是连续的，因为5和7在原数组里被4隔开。 
```
示例 2:
```
输入: [2,2,2,2,2]
输出: 1
解释: 最长连续递增序列是 [2], 长度为1。
```
注意：数组长度不会超过10000。

```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int ans = 0, anchor = 0;
        for (int i = 0; i < nums.length; ++i) {
            if (i > 0 && nums[i-1] >= nums[i]) anchor = i;
            ans = Math.max(ans, i - anchor + 1);
        }
        return ans;
    }
}
```



### <span id='j45'>697. 数组的度</span>
给定一个非空且只包含非负数的整数数组 nums, 数组的度的定义是指数组里任一元素出现频数的最大值。  
你的任务是找到与 nums 拥有相同大小的度的最短连续子数组，返回其长度。  

示例 1:
```
输入: [1, 2, 2, 3, 1]
输出: 2
解释: 
输入数组的度是2，因为元素1和2的出现频数最大，均为2.
连续子数组里面拥有相同度的有如下所示:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
最短连续子数组[2, 2]的长度为2，所以返回2.
```
示例 2:
```
输入: [1,2,2,3,1,4,2]
输出: 6
```
注意:  
nums.length 在1到50,000区间范围内。 
nums[i] 是一个在0到49,999范围内的整数。  

```java
class Solution {
    public int findShortestSubArray(int[] nums) {
        Map<Integer, int[]> numMap = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int[] number = numMap.getOrDefault(nums[i], new int[3]);
            number[0]++;
            if (number[1] == 0) {
                number[1] = i + 1;
            }
            number[2] = i + 1;
            numMap.put(nums[i], number);
        }
        int minLen = 0;
        int count = 0;
        for (int[] value : numMap.values()) {
            if (value[0] > count) {
                count = value[0];
                minLen = value[2] - value[1] + 1;
            } else if (value[0] == count) {
                minLen = Math.min(minLen, value[2] - value[1] + 1);
            }
        }
        return minLen;
    }
}
```



### <span id='j46'>717. 1比特与2比特字符</span>
有两种特殊字符。第一种字符可以用一比特0来表示。第二种字符可以用两比特(10 或 11)来表示。  
现给一个由若干比特组成的字符串。问最后一个字符是否必定为一个一比特字符。给定的字符串总是由0结束。  

示例 1:
```
输入: 
bits = [1, 0, 0]
输出: True
解释: 
唯一的编码方式是一个两比特字符和一个一比特字符。所以最后一个字符是一比特字符。
```
示例 2:
```
输入: 
bits = [1, 1, 1, 0]
输出: False
解释: 
唯一的编码方式是两比特字符和两比特字符。所以最后一个字符不是一比特字符。
```
注意:  
1 <= len(bits) <= 1000.  
bits[i] 总是0 或 1.  

```java
class Solution {
    public boolean isOneBitCharacter(int[] bits) {
        int len = bits.length;
        boolean result = false;
        for(int i=0;i<len;i++){
            if(bits[i] == 0) {
               if(i+1 == len ) result = true;
               continue; 
            }
            if(bits[i] == 1) i++;
        }
        return result;
    }
}
```



### <span id='j47'>724. 寻找数组的中心索引</span>
给定一个整数类型的数组 nums，请编写一个能够返回数组“中心索引”的方法。  
我们是这样定义数组中心索引的：数组中心索引的左侧所有元素相加的和等于右侧所有元素相加的和。  
如果数组不存在中心索引，那么我们应该返回 -1。如果数组有多个中心索引，那么我们应该返回最靠近左边的那一个。  

示例 1:
```
输入: 
nums = [1, 7, 3, 6, 5, 6]
输出: 3
解释: 
索引3 (nums[3] = 6) 的左侧数之和(1 + 7 + 3 = 11)，与右侧数之和(5 + 6 = 11)相等。
同时, 3 也是第一个符合要求的中心索引。
```
示例 2:
```
输入: 
nums = [1, 2, 3]
输出: -1
解释: 
数组中不存在满足此条件的中心索引。
```
说明:
nums 的长度范围为 [0, 10000]。  
任何一个 nums[i] 将会是一个范围在 [-1000, 1000]的整数。  

```java
class Solution {
    public int pivotIndex(int[] nums) {
        int sum = 0, leftsum = 0;
        for (int x: nums) sum += x;
        for (int i = 0; i < nums.length; ++i) {
            if (leftsum == sum - leftsum - nums[i]) return i;
            leftsum += nums[i];
        }
        return -1;
    }
}
```



### <span id='j48'>746. 使用最小花费爬楼梯</span>
数组的每个索引做为一个阶梯，第 i个阶梯对应着一个非负数的体力花费值 cost[i](索引从0开始)。  
每当你爬上一个阶梯你都要花费对应的体力花费值，然后你可以选择继续爬一个阶梯或者爬两个阶梯。  
您需要找到达到楼层顶部的最低花费。在开始时，你可以选择从索引为 0 或 1 的元素作为初始阶梯。  

示例 1:
```
输入: cost = [10, 15, 20]
输出: 15
解释: 最低花费是从cost[1]开始，然后走两步即可到阶梯顶，一共花费15。
```
示例 2:
```
输入: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
输出: 6
解释: 最低花费方式是从cost[0]开始，逐个经过那些1，跳过cost[3]，一共花费6。
```
注意：  
cost 的长度将会在 [2, 1000]。  
每一个 cost[i] 将会是一个Integer类型，范围为 [0, 999]。  

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int f1 = 0, f2 = 0;
        for (int i = cost.length - 1; i >= 0; --i) {
            int f0 = cost[i] + Math.min(f1, f2);
            f2 = f1;
            f1 = f0;
        }
        return Math.min(f1, f2);
    }
}
```
   


### <span id='j49'>747. 至少是其他数字两倍的最大数</span>
在一个给定的数组nums中，总是存在一个最大元素 。  
查找数组中的最大元素是否至少是数组中每个其他数字的两倍。  
如果是，则返回最大元素的索引，否则返回-1。  

示例 1:
```
输入: nums = [3, 6, 1, 0]
输出: 1
解释: 6是最大的整数, 对于数组中的其他整数,
6大于数组中其他元素的两倍。6的索引是1, 所以我们返回1.
```
示例 2:
```
输入: nums = [1, 2, 3, 4]
输出: -1
解释: 4没有超过3的两倍大, 所以我们返回 -1.
```
提示:  
nums 的长度范围在[1, 50].  
每个 nums[i] 的整数范围在 [0, 99].  

```java
class Solution {
    public int dominantIndex(int[] nums) {
        int fmax = 0;
        int sMax = 0;
        int index = -1;
        
        for(int i=0; i<nums.length; i++){
            if(nums[i] > fmax){
                sMax = fmax;
                fmax = nums[i];
                index = i;
            }else if(nums[i] > sMax){
                sMax = nums[i];
            }   
        }
        
        return fmax >= sMax*2 ? index : -1;
        
    }
}
```




### <span id='j50'>766. 托普利茨矩阵</span>
如果一个矩阵的每一方向由左上到右下的对角线上具有相同元素，那么这个矩阵是托普利茨矩阵。  
给定一个 M x N 的矩阵，当且仅当它是托普利茨矩阵时返回 True。  

示例 1:
```
输入: 
matrix = [
  [1,2,3,4],
  [5,1,2,3],
  [9,5,1,2]
]
输出: True
解释:
在上述矩阵中, 其对角线为:
"[9]", "[5, 5]", "[1, 1, 1]", "[2, 2, 2]", "[3, 3]", "[4]"。
各条对角线上的所有元素均相同, 因此答案是True。
```
示例 2:
```
输入:
matrix = [
  [1,2],
  [2,2]
]
输出: False
解释: 
对角线"[1, 2]"上的元素不同。
```
说明:  
matrix 是一个包含整数的二维数组。  
matrix 的行数和列数均在 [1, 20]范围内。  
matrix[i][j] 包含的整数在 [0, 99]范围内。  
进阶:  
如果矩阵存储在磁盘上，并且磁盘内存是有限的，因此一次最多只能将一行矩阵加载到内存中，该怎么办？  
如果矩阵太大以至于只能一次将部分行加载到内存中，该怎么办？  

```java
class Solution {
    public boolean isToeplitzMatrix(int[][] matrix) {
        Map<Integer, Integer> groups = new HashMap();
        for (int r = 0; r < matrix.length; ++r) {
            for (int c = 0; c < matrix[0].length; ++c) {
                if (!groups.containsKey(r-c))
                    groups.put(r-c, matrix[r][c]);
                else if (groups.get(r-c) != matrix[r][c])
                    return false;
            }
        }
        return true;
    }
}
```



### <span id='j51'>830. 较大分组的位置</span>
在一个由小写字母构成的字符串 S 中，包含由一些连续的相同字符所构成的分组。  
例如，在字符串 S = "abbxxxxzyy" 中，就含有 "a", "bb", "xxxx", "z" 和 "yy" 这样的一些分组。  

我们称所有包含大于或等于三个连续字符的分组为较大分组。找到每一个较大分组的起始和终止位置。  
最终结果按照字典顺序输出。  

示例 1:
```
输入: "abbxxxxzzy"
输出: [[3,6]]
解释: "xxxx" 是一个起始于 3 且终止于 6 的较大分组。
```
示例 2:
```
输入: "abc"
输出: []
解释: "a","b" 和 "c" 均不是符合要求的较大分组。
```
示例 3:
```
输入: "abcdddeeeeaabbbcd"
输出: [[3,5],[6,9],[12,14]]
```
说明:  1 <= S.length <= 1000

```java
class Solution {
    public List<List<Integer>> largeGroupPositions(String S) {
        List<List<Integer>> ans = new ArrayList();
        int i = 0, N = S.length(); // i is the start of each group
        for (int j = 0; j < N; ++j) {
            if (j == N-1 || S.charAt(j) != S.charAt(j+1)) {
                // Here, [i, j] represents a group.
                if (j-i+1 >= 3)
                    ans.add(Arrays.asList(new Integer[]{i, j}));
                i = j + 1;
            }
        }

        return ans;
    }
}
```

### <span id='j52'>832. 翻转图像</span>
给定一个二进制矩阵 A，我们想先水平翻转图像，然后反转图像并返回结果。  

水平翻转图片就是将图片的每一行都进行翻转，即逆序。例如，水平翻转 [1, 1, 0] 的结果是 [0, 1, 1]。  
反转图片的意思是图片中的 0 全部被 1 替换， 1 全部被 0 替换。例如，反转 [0, 1, 1] 的结果是 [1, 0, 0]。   

示例 1:
```
输入: [[1,1,0],[1,0,1],[0,0,0]]
输出: [[1,0,0],[0,1,0],[1,1,1]]
解释: 首先翻转每一行: [[0,1,1],[1,0,1],[0,0,0]]；
     然后反转图片: [[1,0,0],[0,1,0],[1,1,1]]
```
示例 2:
```
输入: [[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
输出: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
解释: 首先翻转每一行: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]]；
     然后反转图片: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
```
说明:
1 <= A.length = A[0].length <= 20   
0 <= A[i][j] <= 1   

```java
class Solution {
    public int[][] flipAndInvertImage(int[][] A) {
        if (A == null) return null;
        for (int[] row : A) {
            if (row == null) continue;
            for (int i = 0, j = row.length - 1; i < j; ++i,--j) {
                int t = row[i];
                row[i] = row[j];
                row[j] = t;
            }
            for(int i = 0; i < row.length; ++i) {
                row[i] = row[i] ^ 1;
            }
        }
        return A;
    }
}
```


### <span id='j51'>840. 矩阵中的幻方</span>
3 x 3 的幻方是一个填充有从 1 到 9 的不同数字的 3 x 3 矩阵，其中每行，每列以及两条对角线上的各数之和都相等。  
给定一个由整数组成的 N × N 矩阵，其中有多少个 3 × 3 的 “幻方” 子矩阵？（每个子矩阵都是连续的）。  

示例 1:
```
输入: [[4,3,8,4],
      [9,5,1,9],
      [2,7,6,2]]
输出: 1
解释: 
下面的子矩阵是一个 3 x 3 的幻方：
438
951
276

而这一个不是：
384
519
762

总的来说，在本示例所给定的矩阵中只有一个 3 x 3 的幻方子矩阵。
```
提示:  
1. 1 <= grid.length = grid[0].length <= 10  
2. 0 <= grid[i][j] <= 15  

```java
class Solution {
    public int numMagicSquaresInside(int[][] grid) {
        int R = grid.length, C = grid[0].length;
        int ans = 0;
        for (int r = 0; r < R-2; ++r)
            for (int c = 0; c < C-2; ++c) {
                if (grid[r+1][c+1] != 5) continue;  // optional skip
                if (magic(grid[r][c], grid[r][c+1], grid[r][c+2],
                          grid[r+1][c], grid[r+1][c+1], grid[r+1][c+2],
                          grid[r+2][c], grid[r+2][c+1], grid[r+2][c+2]))
                    ans++;
            }

        return ans;
    }

    public boolean magic(int... vals) {
        int[] count = new int[16];
        for (int v: vals) count[v]++;
        for (int v = 1; v <= 9; ++v)
            if (count[v] != 1)
                return false;

        return (vals[0] + vals[1] + vals[2] == 15 &&
                vals[3] + vals[4] + vals[5] == 15 &&
                vals[6] + vals[7] + vals[8] == 15 &&
                vals[0] + vals[3] + vals[6] == 15 &&
                vals[1] + vals[4] + vals[7] == 15 &&
                vals[2] + vals[5] + vals[8] == 15 &&
                vals[0] + vals[4] + vals[8] == 15 &&
                vals[2] + vals[4] + vals[6] == 15);
    }
}
```


### <span id='j53'>849. 到最近的人的最大距离</span>
在一排座位（ seats）中，1 代表有人坐在座位上，0 代表座位上是空的。  
至少有一个空座位，且至少有一人坐在座位上。  
亚历克斯希望坐在一个能够使他与离他最近的人之间的距离达到最大化的座位上。  
返回他到离他最近的人的最大距离。  

示例 1：
```
输入：[1,0,0,0,1,0,1]
输出：2
解释：
如果亚历克斯坐在第二个空位（seats[2]）上，他到离他最近的人的距离为 2 。
如果亚历克斯坐在其它任何一个空位上，他到离他最近的人的距离为 1 。
因此，他到离他最近的人的最大距离是 2 。
``` 
示例 2：
```
输入：[1,0,0,0]
输出：3
解释： 
如果亚历克斯坐在最后一个座位上，他离最近的人有 3 个座位远。
这是可能的最大距离，所以答案是 3 。
```
提示：
1. 1 <= seats.length <= 20000  
2. seats 中只含有 0 和 1，至少有一个 0，且至少有一个 1。  

```java
class Solution {
    public int maxDistToClosest(int[] seats) {
        int N = seats.length;
        int[] left = new int[N], right = new int[N];
        Arrays.fill(left, N);
        Arrays.fill(right, N);

        for (int i = 0; i < N; ++i) {
            if (seats[i] == 1) left[i] = 0;
            else if (i > 0) left[i] = left[i-1] + 1;
        }

        for (int i = N-1; i >= 0; --i) {
            if (seats[i] == 1) right[i] = 0;
            else if (i < N-1) right[i] = right[i+1] + 1;
        }

        int ans = 0;
        for (int i = 0; i < N; ++i)
            if (seats[i] == 0)
                ans = Math.max(ans, Math.min(left[i], right[i]));
        return ans;
    }
}

```


### <span id='j54'>867. 转置矩阵</span>
给定一个矩阵 A， 返回 A 的转置矩阵。  
矩阵的转置是指将矩阵的主对角线翻转，交换矩阵的行索引与列索引。  

示例 1：
```
输入：[[1,2,3],[4,5,6],[7,8,9]]
输出：[[1,4,7],[2,5,8],[3,6,9]]
```
示例 2：
```
输入：[[1,2,3],[4,5,6]]
输出：[[1,4],[2,5],[3,6]]
```
提示：  
1 <= A.length <= 1000  
1 <= A[0].length <= 1000  

```java
class Solution {
    public int[][] transpose(int[][] A) {
        int R = A.length, C = A[0].length;
        int[][] ans = new int[C][R];
        for (int r = 0; r < R; ++r)
            for (int c = 0; c < C; ++c) {
                ans[c][r] = A[r][c];
            }
        return ans;
    }
}
```


### <span id='j55'>888. 公平的糖果交换</span>
爱丽丝和鲍勃有不同大小的糖果棒：A[i] 是爱丽丝拥有的第 i 块糖的大小，B[j] 是鲍勃拥有的第 j 块糖的大小。  
因为他们是朋友，所以他们想交换一个糖果棒，这样交换后，他们都有相同的糖果总量。（一个人拥有的糖果总量是他们拥有的糖果棒大小的总和。）  
返回一个整数数组 ans，其中 ans[0] 是爱丽丝必须交换的糖果棒的大小，ans[1] 是 Bob 必须交换的糖果棒的大小。  
如果有多个答案，你可以返回其中任何一个。保证答案存在。  

示例 1：
```
输入：A = [1,1], B = [2,2]
输出：[1,2]
```
示例 2：
```
输入：A = [1,2], B = [2,3]
输出：[1,2]
```
示例 3：
```
输入：A = [2], B = [1,3]
输出：[2,3]
```
示例 4：
```
输入：A = [1,2,5], B = [2,4]
输出：[5,4]
```

提示：  
1 <= A.length <= 10000  
1 <= B.length <= 10000  
1 <= A[i] <= 100000  
1 <= B[i] <= 100000  
保证爱丽丝与鲍勃的糖果总量不同。  
答案肯定存在。  

```java
class Solution {
    public int[] fairCandySwap(int[] A, int[] B) {
        int sa = 0, sb = 0;  // sum of A, B respectively
        for (int x: A) sa += x;
        for (int x: B) sb += x;
        int delta = (sb - sa) / 2;
        // If Alice gives x, she expects to receive x + delta

        Set<Integer> setB = new HashSet();
        for (int x: B) setB.add(x);

        for (int x: A)
            if (setB.contains(x + delta))
                return new int[]{x, x + delta};

        throw null;
    }
}
```


### <span id='j56'>896. 单调数列</span>
如果数组是单调递增或单调递减的，那么它是单调的。  
如果对于所有 i <= j，A[i] <= A[j]，那么数组 A 是单调递增的。 如果对于所有 i <= j，A[i]> = A[j]，那么数组 A 是单调递减的。  
当给定的数组 A 是单调数组时返回 true，否则返回 false。  

示例 1：
```
输入：[1,2,2,3]
输出：true
```
示例 2：
```
输入：[6,5,4,4]
输出：true
```
示例 3：
```
输入：[1,3,2]
输出：false
```
示例 4：
```
输入：[1,2,4,5]
输出：true
```
示例 5：
```
输入：[1,1,1]
输出：true
```

提示：  
1 <= A.length <= 50000  
-100000 <= A[i] <= 100000  

```java
class Solution {
    public boolean isMonotonic(int[] A) {
        int store = 0;
        for (int i = 0; i < A.length - 1; ++i) {
            int c = Integer.compare(A[i], A[i+1]);
            if (c != 0) {
                if (c != store && store != 0)
                    return false;
                store = c;
            }
        }

        return true;
    }
}
```


### <span id='j57'>905. 按奇偶排序数组</span>
给定一个非负整数数组 A，返回一个由 A 的所有偶数元素组成的数组，后面跟 A 的所有奇数元素。  
你可以返回满足此条件的任何数组作为答案。  

示例：
```
输入：[3,1,2,4]
输出：[2,4,3,1]
输出 [4,2,3,1]，[2,4,1,3] 和 [4,2,1,3] 也会被接受。
```
提示：  
1 <= A.length <= 5000  
0 <= A[i] <= 5000  

```java
class Solution {
    public int[] sortArrayByParity(int[] A) {
        int[] ans = new int[A.length];
        int t = 0;

        for (int i = 0; i < A.length; ++i)
            if (A[i] % 2 == 0)
                ans[t++] = A[i];

        for (int i = 0; i < A.length; ++i)
            if (A[i] % 2 == 1)
                ans[t++] = A[i];

        return ans;
    }
}
```


### <span id='j58'>914. 卡牌分组</span>
给定一副牌，每张牌上都写着一个整数。  
此时，你需要选定一个数字 X，使我们可以将整副牌按下述规则分成 1 组或更多组：  
每组都有 X 张牌。  
组内所有的牌上都写着相同的整数。  
仅当你可选的 X >= 2 时返回 true。  

示例 1：
```
输入：[1,2,3,4,4,3,2,1]
输出：true
解释：可行的分组是 [1,1]，[2,2]，[3,3]，[4,4]
```
示例 2：
```
输入：[1,1,1,2,2,2,3,3]
输出：false
解释：没有满足要求的分组。
```
示例 3：
```
输入：[1]
输出：false
解释：没有满足要求的分组。
```
示例 4：
```
输入：[1,1]
输出：true
解释：可行的分组是 [1,1]
```
示例 5：
```
输入：[1,1,2,2,2,2]
输出：true
解释：可行的分组是 [1,1]，[2,2]，[2,2]
```
提示：  
1 <= deck.length <= 10000  
0 <= deck[i] < 10000  

```java
class Solution {
    public boolean hasGroupsSizeX(int[] deck) {
        int[] count = new int[10000];
        for (int c: deck)
            count[c]++;

        int g = -1;
        for (int i = 0; i < 10000; ++i)
            if (count[i] > 0) {
                if (g == -1)
                    g = count[i];
                else
                    g = gcd(g, count[i]);
            }

        return g >= 2;
    }

    public int gcd(int x, int y) {
        return x == 0 ? y : gcd(y%x, x);
    }
}
```


### <span id='j59'>922. 按奇偶排序数组 II</span>
给定一个非负整数数组 A， A 中一半整数是奇数，一半整数是偶数。  
对数组进行排序，以便当 A[i] 为奇数时，i 也是奇数；当 A[i] 为偶数时， i 也是偶数。  
你可以返回任何满足上述条件的数组作为答案。  

示例：
```
输入：[4,2,5,7]
输出：[4,5,2,7]
解释：[4,7,2,5]，[2,5,4,7]，[2,7,4,5] 也会被接受。
```
提示：  
2 <= A.length <= 20000  
A.length % 2 == 0  
0 <= A[i] <= 1000  

```java
class Solution {
    public int[] sortArrayByParityII(int[] A) {
        int j = 1;
        for (int i = 0; i < A.length; i += 2)
            if (A[i] % 2 == 1) {
                while (A[j] % 2 == 1)
                    j += 2;

                // Swap A[i] and A[j]
                int tmp = A[i];
                A[i] = A[j];
                A[j] = tmp;
            }

        return A;
    }
}
```


### <span id='j60'>941. 有效的山脉数组</span>
给定一个整数数组 A，如果它是有效的山脉数组就返回 true，否则返回 false。  
让我们回顾一下，如果 A 满足下述条件，那么它是一个山脉数组：  

A.length >= 3  
在 0 < i < A.length - 1 条件下，存在 i 使得：  
    A[0] < A[1] < ... A[i-1] < A[i]  
    A[i] > A[i+1] > ... > A[B.length - 1]  
 
示例 1：
```
输入：[2,1]
输出：false
```
示例 2：
```
输入：[3,5,5]
输出：false
```
示例 3：
```
输入：[0,3,2,1]
输出：true
```
提示：  
0 <= A.length <= 10000  
0 <= A[i] <= 10000   

```java
class Solution {
    public boolean validMountainArray(int[] A) {
        int N = A.length;
        int i = 0;

        // walk up
        while (i+1 < N && A[i] < A[i+1])
            i++;

        // peak can't be first or last
        if (i == 0 || i == N-1)
            return false;

        // walk down
        while (i+1 < N && A[i] > A[i+1])
            i++;

        return i == N-1;
    }
}
```
