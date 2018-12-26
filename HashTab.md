# 目录 
## 简单#HashTab#
+ [136. 只出现一次的数字](#j1)
+ [202. 快乐数](#j2)
+ [204. 计数质数](#j3)




### <span id='j1'>136. 只出现一次的数字</span>
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。  

说明：  
你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？  

示例 1:
```
输入: [2,2,1]
输出: 1
```
示例 2:
```
输入: [4,1,2,1,2]
输出: 4
```

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for(int i=0; i<nums.length; i++ )
            res = res^nums[i];
        return res;
    }
}
```


### <span id='j2'>202. 快乐数</span>
编写一个算法来判断一个数是不是“快乐数”。

一个“快乐数”定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是无限循环但始终变不到 1。如果可以变为 1，那么这个数就是快乐数。

示例: 
![image](https://raw.githubusercontent.com/suifeng412/LeetCode-Algorithms/master/public/2018-12-26_230658.jpg)

```java
// 不是快乐数的数称为不快乐数（unhappy number），所有不快乐数的数位平方和计算，最後都会进入 4 → 16 → 37 → 58 → 89 → 145 → 42 → 20 → 4 的循环中。
class Solution {
    public boolean isHappy(int n) {
        String nums = n + "";
        int num = n;
        while (true) {
			// 为1 说明是快乐数 跳出
			 if (num == 1) {
				 return true;
			// 为4说明肯定不是快乐数，因为会无限循环  4 = 16; 16 = 37 37 = 65	 
			 } else if (num == 4) {
				 return false;
			 } else {
			// 继续循环
				 nums = num + "";
				 num = 0;
			 }
			 for (int i = 0, length = nums.length(); i < length; i++) {
				 int ns = Character.getNumericValue(nums.charAt(i));
				 num += ns*ns;
			 }
		 }
    }
}
```


### <span id='j2'>204. 计数质数</span>
统计所有小于非负整数 n 的质数的数量。  
示例:
```
输入: 10
输出: 4
解释: 小于 10 的质数一共有 4 个, 它们是 2, 3, 5, 7 。
```

```java
class Solution {
    public int countPrimes(int n) {
        if(n < 3)
            return 0;
        boolean[] arr = new boolean[n];
        int count = n/2;
        for(int i = 3;i*i<n;i+=2){
            if(arr[i]) continue;
            for(int j = i*i;j<n;j+=2*i){
                if(!arr[j]){
                     count--;
                    arr[j] = true;
                }
            }
        }
        return count;
    }
}
```
