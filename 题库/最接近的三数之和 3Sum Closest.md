### 最接近的三数之和 3Sum Closest

#### 题目

给定一个包括 *n* 个整数的数组 `nums` 和 一个目标值 `target`。找出 `nums` 中的三个整数，使得它们的和与 `target` 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

示例：

```javascript
例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```

#### 解答

思路1：此题跟`三数之和`思路一致，结果集换成了差值的比较。

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function(nums, target) {
  var result = Infinity;
  nums.sort((a, b) => a - b);
  for(var i = 0; i < nums.length-2; i++){
    if(i > 0 && nums[i] === nums[i-1]) continue;
    for(var j = i+1, k = nums.length - 1; j < k;){
      var temp = nums[i] + nums[j] + nums[k];
      if(temp === target){
        return target;
      } else if (temp < target) {
        j++;
        while(j < k && nums[j] === nums[j-1]) { j++ };
      } else {
        k--;
        while(j < k && nums[k] === nums[k+1]) { k-- };
      }
      result = Math.abs(temp - target) > Math.abs(result - target) ? result : temp;
    }
  }
  return result;
};
```

值得注意的是，本来想着将数组去重再循环，但是需要考虑到如果数组项都一致或者去重之后数组长度小于3，就会出现问题。