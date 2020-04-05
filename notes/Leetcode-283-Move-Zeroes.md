# LeetCode 283 - Move elements 

# **From** 
1. [move zeroes](https://leetcode-cn.com/problems/move-zeroes/)

<!-- more -->
# **Problem**


给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:

输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。


2020/3/29 

纯小白， 拿到题目 5分钟不太会， 看了 答题区一些人的答案， 不太懂， 然后又在b站上看到了 这位 [前辈的视频](https://www.bilibili.com/video/BV1XJ41157Eb?from=search&seid=16325579222567466791) ： 懂了一点  


所以开始仿写了一遍 ；


```
public class MoveZeroes {
	public void moveZeroes(int[] nums) {
		int k = 0;
		for (int i = 0; i < nums.length; i ++) {
			if (nums[i] != 0) {
				nums[k] = nums[i];
				k ++;
			}
		}

		for (int j = k; j < nums.length; j ++) {
			nums[j] = 0;
		}
	}
}



//   1. 先遍历数组， 然后 如果遍历到的数组的元素是非0的就 和 下标为k对的数组元素 交换， 这样 可以确保 非0元素的顺序性， 同时  交换后 K 向右移动一位， 保证  下标为k的元素是 第一个0 元素 ， k 前面都是 非0的元素。 




Python 版本如下：

class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
    	k = 0
    	for e in range(len(nums)):
    		if (e):
    			nums[k] = nums[e]
    			k = k + 1
    	for d in range(k,len(nums)):
    		d = 0




```
可以看见  用了 两个for循环，   时间复杂度为  O(n), 没有创建新数组，所以空间复杂度为O(1)


但是  提交的结果不太理想： 内存消耗 :42 MB, 在所有 Java 提交中击败了5.10%的用户


所以肯定有待改进