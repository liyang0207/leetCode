### 四数之和 4Sum

#### 题目

给定一个包含 *n* 个整数的数组 `nums` 和一个目标值 `target`，判断 `nums` 中是否存在四个元素 *a，**b，c* 和 *d* ，使得 *a* + *b* + *c* + *d* 的值与 `target` 相等？找出所有满足条件且不重复的四元组。

示例：

```javascript
给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

#### 解答

思路：又是一道跟`三数之和`一模一样套路的题目，吐。。。

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[][]}
 */
var fourSum = function(nums, target) {
  var result = [];
  nums.sort((a, b) => a - b);
  console.log(nums)
  for(var i = 0; i < nums.length - 3; i++){
    if(i > 0 && nums[i] === nums[i-1]) continue;
    for(var j = i+1; j < nums.length - 2; j++){
      if(j > i+1 && nums[j] === nums[j-1]) continue;
      for(var k = j+1, q = nums.length - 1; k < q;){
        var temp = nums[i] + nums[j] + nums[k] + nums[q];
        if(temp === target){
          result.push([nums[i], nums[j], nums[k], nums[q]]);
          k++;q--;
          while(k < q && nums[k] === nums[k-1]){ k++; }
          while(k < q && nums[q] === nums[q+1]){ q--; }
        }else if(temp < target) {
          k++;
        }else{
          q--;      
        }
      }
    }
  }
  return result;
};
```

无趣，连着3道题解题思路一致，难不成每道题各有不同的优秀解？