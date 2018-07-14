### 数组拆分 I Array Partition I

#### 题目

给定长度为 **2n** 的数组, 你的任务是将这些数分成 **n** 对, 例如 (a1, b1), (a2, b2), ..., (an, bn) ，使得从1 到 n 的 min(ai, bi) 总和最大。 

示例：

```javascript
输入: [1,4,3,2]

输出: 4
解释: n 等于 2, 最大总和为 4 = min(1, 2) + min(3, 4).。
```

**提示:**

1. **n** 是正整数,范围在 [1, 10000].
2. 数组中的元素范围在 [-10000, 10000].

#### 解答

思路1： 先排序，然后间隔取值相加。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var arrayPairSum = function(nums) {
  var result = 0, len = nums.length;
  nums.sort((a, b) => { return a - b; });
  for(var i = 0; i < len; i++){
    result += nums[i];
    i++;
  }
  return result;
};
```

提交通过。吐槽一下国内服务器，一直无法提交，以为自己解答错误，切到英文版，提交通过。纠结要不要换成英文版。

