### 最大连续1的个数 Max Consecutive Ones 

#### 题目

给定一个二进制数组， 计算其中最大连续1的个数。 

示例：

```javascript
输入: [1,1,0,1,1,1]
输出: 3
解释: 开头的两位和最后的三位都是连续1，所以最大连续1的个数是 3.
```

**注意：**

- 输入的数组只包含 `0` 和`1`。
- 输入数组的长度是正整数，且不超过 10,000。

标签：`数组`

#### 解答

思路1：定义变量max记录最大值，flag变量来记录每一次连续`1`的数量，遇到`0`就重置。循环数组。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMaxConsecutiveOnes = function(nums) {
  var len = nums.length, flag = 0, max = 0;
  for(var i = 0; i < len; i++){
    if(nums[i] === 1){
      flag++;
      max = Math.max(flag, max);
    }else{
      flag = 0;
    }
  }
  return max;
};
```

提交通过，基本上解答都是这个思路。