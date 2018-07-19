### 两个数组的交集 II Intersection of Two Arrays II  

#### 题目

给定两个数组，写一个方法来计算它们的交集。 

示例：

```javascript
给定 nums1 = [1, 2, 2, 1], nums2 = [2, 2], 返回 [2, 2]
```

**注意：**

-    输出结果中每个元素出现的次数，应与元素在两个数组中出现的次数一致。
-    我们可以不考虑输出结果的顺序。

**跟进:**

- 如果给定的数组已经排好序呢？你将如何优化你的算法？
- 如果 *nums1* 的大小比 *nums2* 小很多，哪种方法更优？
- 如果*nums2*的元素存储在磁盘上，内存是有限的，你不能一次加载所有的元素到内存中，你该怎么办？

标签：`排序` `哈希表` `双指针` `二分查找`

#### 解答

思路1：跟`两个数组的交集`题目基本一样，只不过在数组2找到值之后将该值切掉，再接着找就可以了。

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersect = function(nums1, nums2) {
  var result = [], flag = 0;
  for(var i = 0; i < nums1.length; i++){
    var idx = nums2.indexOf(nums1[i])
    if(idx > -1){
      result.push(nums1[i]);
      nums2.splice(idx, 1);
    }
  }
  return result;
};
```

提交通过，性能可以。









