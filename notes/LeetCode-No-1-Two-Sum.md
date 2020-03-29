---
title: LeetCode No.1 Two Sum
tags:
  - LeetCode
  - Array
categories:
  - LeetCode
abbrlink: 251993f5
date: 2019-10-06 15:27:36
---

# **From** 
1. [Two Sum](https://leetcode.com/problems/two-sum/#/description)

<!-- more -->
# **Problem**
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

这里的indice指的是  数组下标

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/two-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


# **Example**

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].


# **Solutions**

1. 第一种方法

根据题目， 最简单的方法是 遍历两遍数组， 每次判断 是否和为指定的值。

```
class Solution {
    public static int[] twoSum(int[] nums, int target) {
        int[] array = new int[2];
        for (int i = 0; i < nums.length; i ++) {
            for (int j = i + 1; j < nums.length; j ++) {
                if (nums[i] + nums[j] == target) {
                    array[0] = i;
                    array[1] =  j;
                }
            }
        }
        return array;    
    }
    public static void main(String[] args) {
        int[] nums = [2,7,11,15];
        int target = 9;
        System.out.println(Arrays.toString(twoSum(nums)));

// 注意了， 不能直接print array, 这是因为"arr"指向的是这个数组对象在内存中的地址，而不是数组的内容。如果你直接这样打印，输出的结果是一串字母+数字的字符串，这个字符串就是该数组对象的内存地址。

所以必须转换为字符串输出，

java里，所有的类，不管是java库里面的类，或者是你自己创建的类，全部是从object这个类继承的。object里有一个方法就是toString()，那么所有的类创建的时候，都有一个toString的方法。这个方法是干什么的呢？ 
　　首先我们得了解，java输出用的函数print();是不接受对象直接输出的，只接受字符串或者数字之类的输出。 
　　当print检测到输出的是一个对象而不是字符或者数字时，那么它会去调用这个对象类里面的toString 方法，输出结果为[类型@哈希值]。Object类中的toString()方法的源代码如下：



    }
}
```
上面这种方法的时间复杂度很高，两层循环达到了 O(N^2)



2. 第二种方法

为了减少时间复杂度， 可以考虑用空间换取时间

考虑到map 的查询都是常数级别的， 所以引入Map, 用来存储数组值和下标的关系

**具体思路**


1. 遍历数组
2. 保存数组的值和索引映射关系map
3. 根据当前的值 和 target 找出 map中是否存在对应的key
4. 若存在， 直接得到结果并返回

使用hashmap， key 为数组的值， value 为数组的下标

```

import java.util.Map;
import java.util.HashMap;
import java.util.Arrays;

public class ClassNameHere {
   public static int[] twosum(int[] array, int target) {
      Map<Integer, Integer> map = new HashMap<>(array.length);
      int[] twosum = new int[2];
      for (int i = 0; i < array.length; i ++) {
         if (map.containsKey(target - array[i])) {
            twosum[0] = map.get(target - array[i]);
            twosum[1] = i;
            break; //直接退出这个for循环
             }
         else {
            map.put(array[i],i);
            
         
              }
      
      
      
           }
      return twosum;
   
   
   }
   public static void main(String[] args) {
      int[] array = {2,7,8,11};
      int target = 9;
      System.out.println(Arrays.toString(twosum(array, target)));
   }
}

```





