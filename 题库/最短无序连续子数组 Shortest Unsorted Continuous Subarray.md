### 最短无序连续子数组 Shortest Unsorted Continuous Subarray 

#### 题目

给定一个整数数组，你需要寻找一个**连续的子数组**，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

你找到的子数组应是**最短**的，请输出它的长度。

示例：

```javascript
输入: [2, 6, 4, 8, 10, 9, 15]
输出: 5
解释: 你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
```

**说明 :**

1. 输入的数组长度范围在 [1, 10,000]。
2. 输入的数组可能包含**重复**元素 ，所以**升序**的意思是**<=。**

#### 解答

思路1： 先将数组排序，然后对比原数组和排序后的数组，正向和反向循环，记录开始、结束不一样的项，返回长度。注意，`sort()`方法返回排序后的数组，但是也会影响原数组。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var findUnsortedSubarray = function(nums) {
  var source = nums.slice(0), start = 0, end = 0, len = nums.length;
  nums.sort((a, b) => { return a - b; });
  for(var i = 0; i < len; i++){
    if(nums[i] !== source[i]){
      start = i;
      break;
    }
  }
  for(var j = len-1; j > start; j--){
    if(nums[j] !== source[j]){
      end = j;
      break;
    }
  }
  return end - start === 0 ? 0 : end -start + 1;
};
```

提交通过。

