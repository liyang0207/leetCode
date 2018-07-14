### 数组中的K-diff数对 K-diff Pairs in an Array

### 题目

给定一个整数数组和一个整数 **k**, 你需要在数组里找到**不同的** k-diff 数对。这里将 **k-diff** 数对定义为一个整数对 (i, j), 其中 **i** 和 **j** 都是数组中的数字，且两数之差的绝对值是 **k**. 

示例：

```javascript
输入: [3, 1, 4, 1, 5], k = 2
输出: 2
解释: 数组中有两个 2-diff 数对, (1, 3) 和 (3, 5)。
尽管数组中有两个1，但我们只应返回不同的数对的数量。
```

**注意:**

1. 数对 (i, j) 和数对 (j, i) 被算作同一数对。
2. 数组的长度不超过10,000。
3. 所有输入的整数的范围在 [-1e7, 1e7]。

### 解答

思路1： 这道题需要考虑到的一点就是，`1,2`和`2,1`算是同一数对儿。考虑双循环，使用map表存下匹配的数对儿，这里的key值做个转化，将小值放前，大值放后，这样可以避免重复数对。

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findPairs = function(nums, k) {
  var flag = 0, len = nums.length, map = {};
  for(var i = 0; i < len - 1; i++){
    for(var j = i+1; j < len; j++){
      if(Math.abs(nums[j] - nums[i]) === k){
        var key = Math.min(nums[j], nums[i]).toString() + Math.max(nums[j], nums[i]).toString();
        if(!map[key]){
          map[key] = true;
          flag ++
        }
      }
    }
  }
  return flag;
};
```

提交通过，但是提交记录里思路偏差巨大，不同的思路运行效率相差很多。以后再好好考虑考虑。





































