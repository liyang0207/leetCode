### 最大子序和 Maximum Subarray

#### 题目

给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。 

示例：

```javascript
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

标签： `数组` `分治算法` `动态规划`

#### 解答

思路1：这道题难到了我，最大连续子序和，长度不确定，单纯的看下一个元素的正负无法决定大小，最大的子序不一定会包括最大数组项，标签提示可以使用分治算法，但是不懂什么是分治算分，目前只能暴力计算：循环取数组值，内侧循环不断累加各项，每一次外层循环将最大值存入结果数组，最后找结果数组的最大项。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
  var result = [], flag;
  for (var i = 0; i < nums.length - 1; i++) {
    flag = nums[i];
    result[i] = flag;
    for (var j = i + 1; j < nums.length; j++) {
      flag += nums[j];
      if(result[i] < flag){ 
        result[i] = flag;
      }
    }
  }
  result.push(nums[nums.length - 1]);
  return result.sort(function(a, b){
    return a - b;
  })[result.length - 1];
};
```

结果虽然可以通过，但是效率惨不忍睹，查看比较优秀的解答，不太明白其中的逻辑，关于分治算法需要多做几题才能明白。

思路2：暂时无法理解逻辑，等理解分治算法回过头来思考。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function (nums) {
    let count = nums[0], maxCount = nums[0]
    for (let i = 1; i < nums.length; i++) {
        count = Math.max(count + nums[i], nums[i])
        maxCount = Math.max(maxCount, count)    
    }
    return maxCount
};
```











