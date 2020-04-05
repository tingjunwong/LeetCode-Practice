


# **From** 
1. [single number](https://leetcode-cn.com/problems/single-number-ii)

<!-- more -->
# **Problem**
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现了三次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:

输入: [2,2,3,2]
输出: 3
示例 2:

输入: [0,1,0,1,0,1,99]
输出: 99



这道题  是 leetcode 136 的升级版，  也是采用与异或相似的解法 不过这次 是  3进制，  不能套用异或，

小白日常 不会， 上午看discussion的讨论区也发现  如同天书，看不懂， 于是  在 b站， 微信文章， 知乎， leetcode 题解上 切换， 看到一位前辈的答案 ， 明白了点门道，  


前辈是这样写的：https://leetcode-cn.com/problems/single-number-ii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--31/

```

假如例子是 1 2 6 1 1 2 2 3 3 3, 3 个 1, 3 个 2, 3 个 3,1 个 6
1 0 0 1
2 0 1 0 
6 1 1 0 
1 0 0 1
1 0 0 1
2 0 1 0
2 0 1 0
3 0 1 1  
3 0 1 1
3 0 1 1      
看最右边的一列 1001100111 有 6 个 1
再往前看一列 0110011111 有 7 个 1
再往前看一列 0010000 有 1 个 1
我们只需要把是 3 的倍数的对应列写 0，不是 3 的倍数的对应列写 1    
也就是 1 1 0,也就是 6。

原因的话，其实很容易想明白。如果所有数字都出现了 3 次，那么每一列的 1 的个数就一定是 3 的倍数。之所以有的列不是 3 的倍数，就是因为只出现了 1 次的数贡献出了 1。所以所有不是 3 的倍数的列写 1，其他列写 0 ，就找到了这个出现 1 次的数。



这里为了加深对 leetcode 137的理解，我们将 leetcode 136的内容也搬过来， 与leetcode 137形成对比。


leetcode 函数
public int singleNumber(int[] nums) {
int ans = 0;
if (nums.length > 1) {
	for (int i = 0; i < nums.length; i ++) {
		ans = ans ^ nums[i];
	}
}
return ans;
}

我们可以看到 三进制主要多了一个32位循环 ， 因为二进制 是 人类和计算机已经制定好的约定，所以不需要我们再去构建了，直接默认  异或就是二进制运算。 

而三进制需要先遍历  数组中不同元素相同位，得出有多少个1， 然后 再 在if 语句中 设定 规则 



public int singleNumberII(int[] nums) {
    int ans = 0;
    //考虑每一位
    for (int i = 0; i < 32; i++) {
        int count = 0;
        //考虑每一个数
        for (int j = 0; j < nums.length; j++) {
            //当前位是否是 1
            if ((nums[j] >>> i & 1) == 1) {    
                count++;
            }
        }
        //1 的个数是否是 3 的倍数       				如果是N 进制， 只用 将这里的 3 改成 N，即可，  
        if (count % 3 != 0) {                       
            ans = ans | 1 << i;  				//相当于设置 ans 这个数的第i位 是 1
        }
    }
    return ans;
}

时间复杂度：O（n）。

空间复杂度：O（1）。



再来回顾下题目，题目说是  一堆 N 个相同的数  加上一个 数， 所以不用考虑中间态  意思是  3*n + 2, 3*n+1 这里都是 count % 3 != 0的情况， 

作者：windliang
链接：https://leetcode-cn.com/problems/single-number-ii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--31/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。




```


我一开始想  如果个数为1 个的数 是 0， 会有影响吗， 后来发现没影响，  因为 这样加起来最终每个位都是0， 所以 结果仍然是等于 个数为1 的数 ， 即 0000.....0000(32个0 )