### 最长连续递增序列 Longest Continuous Increasing Subsequence 

### 题目

给定一个未经排序的整数数组，找到最长且**连续**的的递增序列。 

示例：

```javascript
输入: [1,3,5,4,7]
输出: 3
解释: 最长连续递增序列是 [1,3,5], 长度为3。
尽管 [1,3,5,7] 也是升序的子序列, 但它不是连续的，因为5和7在原数组里被4隔开。 

输入: [2,2,2,2,2]
输出: 1
解释: 最长连续递增序列是 [2], 长度为1。
```

**注意：**数组长度不会超过10000。 

标签： `数组`

#### 解答

思路1：循环数组，比较当前项与下一项，决定数量加一还是归0，注意判断数组长度为0时返回0。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var findLengthOfLCIS = function(nums) {
  var len = nums.length, max = 0, flag = 0;
  if(len === 0) return 0;
  for(var i = 0; i < len - 1; i++){
    if(nums[i] < nums[i+1]){
      flag++;
      max = Math.max(flag, max);
    }else{
      flag = 0;
    }
  }
  return max + 1;
};
```

提交通过。

