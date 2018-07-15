### 三个数的最大乘积  Maximum Product of Three Numbers 

#### 题目

 给定一个整型数组，在数组中找出由三个数组成的最大乘积，并输出这个乘积。 

示例：

```javascript
输入: [1,2,3]
输出: 6

输入: [1,2,3,4]
输出: 24
```

**注意:**

1. 给定的整型数组长度范围是[3,104]，数组中所有的元素范围是[-1000, 1000]。
2. 输入的数组中任意三个数的乘积不会超出32位有符号整数的范围。

标签： `数组` `数学`

#### 解答

思路1： 这道题粗看很简单，排序一下数组，直接输出最大3个数的乘积不就ok了，不过有两个地方需要注意：一个是要考虑乘积的大小会不会超出整型范围，另一个是要考虑两个负数相乘可是正数啊，给自己的数学知识跪了，怎么就没考虑到这种情况。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maximumProduct = function(nums) {
  nums.sort((a, b) => { return b - a; });
  var len = nums.length;
  var max1 = nums[0] * nums[1] * nums[2];
  var max2 = nums[0] * nums[len - 1] * nums[len - 2];
  return Math.max(max1, max2);
};
```

提交通过。