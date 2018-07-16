### 子数组最大平均数 I Maximum Average Subarray I 

### 题目

给定 `n` 个整数，找出平均数最大且长度为 `k` 的连续子数组，并输出该最大平均数。 

示例：

```javascript
输入: [1,12,-5,-6,50,3], k = 4
输出: 12.75
解释: 最大平均数 (12-5-6+50)/4 = 51/4 = 12.75
```

**注意:**

1. 1 <= `k` <= `n` <= 30,000。
2. 所给数据范围 [-10,000，10,000]。

标签： `数组`

#### 解答

思路1：两层循环，每次内循环将后面的`k`个数求和，求出平均数，然后不断覆盖最大值。

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findMaxAverage = function(nums, k) {
  var len = nums.length, sum, average = 0, max;
  for(var i = 0; i < len-k+1; i++){
    sum = 0;
    for(var j = i; j < i+k; j++){
      sum += nums[j];
    }
    average = sum / k;
    if(!max) max = average;
    max = Math.max(max, average);
  }
  return max;
};
```

提交通过，但是性能很差，双循环，不好。查看优秀解答，发现一个比较好的思路。

思路2：两次循环，第一次先求出前`k`项和，然后第二次循环从`k`开始，每次加上下一项，同时减去`i-k`项。最后找到和最大的`k`项，再去求平均。这样一方面将双循环降到了单循环，另一方面将求平均放到了最后，思路清晰，性能不错。

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findMaxAverage = function(nums, k) {
  var len = nums.length, sum = 0, max;
  for(var i = 0; i < k; i++){
    sum += nums[i];
    max = sum;
  }
  for(var j = k; j < len; j++){
    sum = sum + nums[j] - nums[j-k];
    max = Math.max(sum, max);
  }
  return max / k
};
```

这个思路很好，`k`项求和如同火车一般不断开向末尾。