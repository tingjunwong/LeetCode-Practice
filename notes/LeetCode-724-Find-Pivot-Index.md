LeetCode-724-Find-Pivot-Index.md



# LeetCode 724 - Find Pivot Index 

# **From** 
1. [move zeroes](https://leetcode.com/problems/find-pivot-index/)

<!-- more -->
# **Problem**


Given an array of integers nums, write a method that returns the "pivot" index of this array.

We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index


Example 2:

Input: 
nums = [1, 2, 3]
Output: -1
Explanation: 
There is no index that satisfies the conditions in the problem statement.
 

Note:

The length of nums will be in the range [0, 10000].
Each element nums[i] will be an integer in the range [-1000, 1000].


2020/3/30   


小白刷题第二天， 拿到题目  ，一开始的思路是 类似于快速排序的思想，   从左侧第一个元素(即下标为0的元素） 开始， 此时 左侧元素之和为0 ， 右侧元素之和为 除左边第一个元素之外的 数组之和，   然后 指针不断遍历整个数组， 一直遍历到  左侧最后一个元素，此时  左侧元素之和 为 除最右边一个元素 之外 的所有元素之和。


```

1. first define  three variables,  sum ,sumLeft, sumRight.


public int pivotIndex(int[] nums) {
	int sum=0,sumLeft = 0, sumRight = 0;

	for (int n : nums) {
		sum = sum + n;      
	}


2.  set the cursor i  , it represents the possible pivot index


	for (int i = 0; i < nums.length; i ++) {
		if (i != 0) {
			sumLeft = sumLeft + nums[i-1];
		}

		sumRight = sum - sumLeft - nums[i];
		if (sumLeft == sumRight) {
			return i;
		}
	}
	return -1;


}


```
其实写完后不难发现， 如果存在pivot index的话 ， 那么左边的和的两倍， 加上中心索引的值， 即等于 数组和，  这是因为   右边的和 =  数组和 - 左边的和 - 中心索引的值， 所以 改进如下：



```

just define two variables  , sumLeft and sum


public int pivotIndex(int[] nums) {
	int sumLeft = 0, sum = 0;
	for (int n : nums) {
		sum += n;
	}
	for (int i = 0; i < nums.length; i ++) {
		if (i != 0) {
			sumLeft += nums[i-1];
		}
		if (2 * sumLeft + nums[i] == sum) {
			return i;
		}
	}
	return -1;

}



```




