### 两个数组的交集 Intersection of Two Arrays 

#### 题目

 给定两个数组，写一个函数来计算它们的交集。 

示例：

```javascript
 给定 num1= [1, 2, 2, 1], nums2 = [2, 2], 返回 [2]
```

**提示:**

- 每个在结果中的元素必定是唯一的。
- 我们可以不考虑输出结果的顺序。

`排序` `哈希表` `双指针` `二分查找`

#### 解答

思路1：数组交集，不能重复元素，使用set，循环一次。

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
  var result = new Set();
  for(var i = 0; i < nums1.length; i++){
    if(nums2.indexOf(nums1[i]) > -1){
      result.add(nums1[i]);
    }
  }
  return [...result.values()];
};
```

提交通过，性能可以。









