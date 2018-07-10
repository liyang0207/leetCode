### 两数之和 II - 输入有序数组 Two Sum II Input Array is Sorted

#### 题目

给定一个已按照**升序排列** 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2*。*

**说明:**

- 返回的下标值（index1 和 index2）不是从零开始的。
- 你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

示例：

```javascript
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

标签： `数组` `双指针` `二分查找`

#### 解答

思路1： 这题思路跟`两数之和`的思路一样，直接使用map表，循环数组，建立`结果-索引`的对应关系。

```javascript
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(numbers, target) {
  var map = {}, j = 0;
  for(var i = 0; i < numbers.length; i++){
    j = map[target - numbers[i]];
    if(j != null){
      return [j+1, i+1];
    }
    map[numbers[i]] = i;
  }
};
```

提交通过，但是标签给了`双指针` `二分查找`，目前不太理解怎么解答。