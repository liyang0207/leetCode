### 搜索插入位置 Search Insert Position

#### 题目

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。 

你可以假设数组中无重复元素。 

示例：

```javascript
输入: [1,3,5,6], 5
输出: 2

输入: [1,3,5,6], 2
输出: 1

输入: [1,3,5,6], 7
输出: 4

输入: [1,3,5,6], 0
输出: 0
```

标签： `数组` `二分查找`

思路1：直接for循环，当目标值小于数组某一项时，将这一项的位置顶替，此时项的index值就为结果索引值。如果没有找到的话，那目标值比数组中任一项都大，返回数组长度即可。

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
  for (let i = 0; i < nums.length; i++ ) {
    if(target <= nums[i]){
      return i;
    }
  }
  return nums.length;
};
```

写的时候很乱，结果出来后慢慢整理才能显得比较简洁，还是大量的锻炼去整理凌乱的思路，慢慢抽出最主要的部分。什么是二分查找还是一脸懵。