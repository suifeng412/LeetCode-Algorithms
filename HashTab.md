# 目录 
## 简单#HashTab#
+ [136. 只出现一次的数字](#j1)
+ [202. 快乐数](#j2)
+ [204. 计数质数](#j3)
+ [205. 同构字符串](#j4)
+ [242. 有效的字母异位词](#j5)
+ [290. 单词模式](#j6)
+ [349. 两个数组的交集](#j7)
+ [350. 两个数组的交集 II](#j8)




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


### <span id='j4'>205. 同构字符串</span>
给定两个字符串 s 和 t，判断它们是否是同构的。  
如果 s 中的字符可以被替换得到 t ，那么这两个字符串是同构的。  
所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。  

示例 1:
```
输入: s = "egg", t = "add"
输出: true
```
示例 2:
```
输入: s = "foo", t = "bar"
输出: false
```
示例 3:
```
输入: s = "paper", t = "title"
输出: true
```
说明:  
你可以假设 s 和 t 具有相同的长度。  

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        Map<Character, Character> sMap = new HashMap<>();
        Map<Character, Character> tMap = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            char sE = s.charAt(i);
            char tE = t.charAt(i);
            Character sVal = sMap.get(sE);
            if (sVal == null) {
                if (tMap.containsKey(tE)) {
                    return false;
                }
                sMap.put(sE, tE);
                tMap.put(tE, sE);
                continue;
            }
            if (sVal != tE) {
                return false;
            }
        }
        return true;
    }
}
```


### <span id='j5'>242. 有效的字母异位词</span>
给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的一个字母异位词。  

示例 1:
```
输入: s = "anagram", t = "nagaram"
输出: true
```
示例 2:
```
输入: s = "rat", t = "car"
输出: false
```
说明:  
你可以假设字符串只包含小写字母。  

进阶:  
如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？  

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        int[] counter = new int[26];
        for (int i = 0; i < s.length(); i++) {
            counter[s.charAt(i) - 'a']++;
            counter[t.charAt(i) - 'a']--;
        }
        for (int count : counter) {
            if (count != 0) {
                return false;
            }
        }
        return true;
    }
}
```


### <span id='j6'>290. 单词模式</span>
给定一种 pattern(模式) 和一个字符串 str ，判断 str 是否遵循相同的模式。  
这里的遵循指完全匹配，例如， pattern 里的每个字母和字符串 str 中的每个非空单词之间存在着双向连接的对应模式。  

示例1:
```
输入: pattern = "abba", str = "dog cat cat dog"
输出: true
```
示例 2:
```
输入:pattern = "abba", str = "dog cat cat fish"
输出: false
```
示例 3:
```
输入: pattern = "aaaa", str = "dog cat cat dog"
输出: false
```
示例 4:
```
输入: pattern = "abba", str = "dog dog dog dog"
输出: false
```
说明:  
你可以假设 pattern 只包含小写字母， str 包含了由单个空格分隔的小写字母。   

```java
class Solution {
    public boolean wordPattern(String pattern, String str) {
        String[] arr = str.split(" ");
        if(pattern.length() != arr.length) return false;
        Map<Character,String> map = new HashMap<>();
        for(int i = 0;i < pattern.length();i++)
        {
            if(map.containsKey(pattern.charAt(i)))
            {
                //包含key的情况，要检查对应的value是否一致
                if(!map.get(pattern.charAt(i)).equals(arr[i])){
                    return false;
                }
            }
            else
            {
                //不包含key的情况下已经有了对应的value，对应到示例4的错误
                if(map.containsValue(arr[i])){
                    return false;
                }
                else
                {
                    map.put(pattern.charAt(i),arr[i]);
                }
            }
        }
        return true;
    }
}
```


### <span id='j7'>349. 两个数组的交集</span>
给定两个数组，编写一个函数来计算它们的交集。  

示例 1:
```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2]
```
示例 2:
```
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [9,4]
```
说明:  
输出结果中的每个元素一定是唯一的。  
我们可以不考虑输出结果的顺序。  

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Set<Integer> set2 = new HashSet<>();

        for (int i = 0; nums1 != null && i < nums1.length; i++) {
            set.add(nums1[i]);
        }
        for (int i = 0; nums2 != null && i < nums2.length; i++) {
            if (set.contains(nums2[i])) {
                set2.add(nums2[i]);
            }
        }

        if (set2.isEmpty()) {
            return new int[0];
        }

        int[] res = new int[set2.size()];
        Iterator<Integer> iterator = set2.iterator();
        int idx = 0;
        while (iterator.hasNext()) {
            res[idx++] = iterator.next();
        }

        return res;
    }
}
```


### <span id='j8'>350. 两个数组的交集 II</span>
给定两个数组，编写一个函数来计算它们的交集。  

示例 1:
```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2,2]
```
示例 2:
```
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [4,9]
```
说明：  
* 输出结果中每个元素出现的次数，应与元素在两个数组中出现的次数一致。
* 我们可以不考虑输出结果的顺序。

进阶:  
* 如果给定的数组已经排好序呢？你将如何优化你的算法？
* 如果 nums1 的大小比 nums2 小很多，哪种方法更优？
* 如果 nums2 的元素存储在磁盘上，磁盘内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
         Map<Integer, Integer> map1 = new HashMap<>();
        for (Integer num : nums1)
            if (map1.containsKey(num))
                map1.replace(num, map1.get(num) + 1);
            else
                map1.put(num, 1);

        ArrayList<Integer> intersection = new ArrayList<>(16);
        for (Integer num : nums2) {
            if (map1.containsKey(num) && map1.get(num) > 0) {
                intersection.add(num);
                map1.replace(num, map1.get(num) - 1);
            }
        }

        int[] ret = new int[intersection.size()];
        for (int i = 0; i < intersection.size(); i++)
            ret[i] = intersection.get(i);
        return ret;
    }
}
```
