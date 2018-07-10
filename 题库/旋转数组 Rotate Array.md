### 旋转数组 Rotate Array 

#### 题目

给定一个数组，将数组中的元素向右移动 *k* 个位置，其中 *k* 是非负数。 

示例：

```javascript
输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]

输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释: 
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]
```

说明：

- 尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
- 要求使用空间复杂度为 O(1) 的原地算法。

标签： `数组` 

#### 解答

思路1： 只能操作原数组，循环k次，每次删除数组最后一项，添加到开头。

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var rotate = function(nums, k) {
  var len = nums.length;
  for(var i =0; i < k; i++){
    nums.unshift(nums.pop());
  }
};
```

提交通过，感觉方法还可以。

思路2：直接删除最后k项，添加到队首。

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var rotate = function(nums, k) {
  var newArr = nums.splice(nums.length - k, k);
  nums.splice(0, 0, ...newArr);
};
```

