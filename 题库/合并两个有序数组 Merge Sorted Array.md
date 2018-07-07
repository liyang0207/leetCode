### 合并两个有序数组 Merge Sorted Array

#### 题目

给定两个有序整数数组 *nums1* 和 *nums2*，将 *nums2* 合并到 *nums1* 中*，*使得 *num1* 成为一个有序数组。

**说明:**

- 初始化 *nums1* 和 *nums2* 的元素数量分别为 *m* 和 *n*。
- 你可以假设 *nums1* 有足够的空间（空间大小大于或等于 *m + n*）来保存 *nums2* 中的元素。

示例：

```javascript
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

标签： `数组` `双指针`

#### 解答

思路1：这道题恶心在`nums1`中可能还有`0`元素，但是题目又指定是有序数组，`0`难道比其他数还大？要排到最后？最后`nums1`中还不能有`0`的存在，而且还只能在`nums1`上操作，简直搞不明白为什么做这么多限制。思路就是先把`0`给切掉，双for循环，针对每一个`nums2`中的元素，去插入到`nums1`中，还要考虑到`nums1`为空或者为`[0]`的情况。

```javascript
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function(nums1, m, nums2, n) {
  var flag = 0;
  nums1.splice(m);
  for (var i = 0; i < n; i++) {
    if (nums1.length < 1) {
      nums1.push(nums2[i]);
      continue;
    }
    if(nums2[i] > nums1[nums1.length - 1]){
      nums1.push(nums2[i]);
      continue;
    }
    for (var j = flag; j < nums1.length; j++) {
      if (nums2[i] <= nums1[j]) {
        nums1.splice(j, 0, nums2[i]);
        flag = j;
        break;
      }
    }
  }
};
```

提交通过，一方面要考虑到`nums1`切过之后为空的情况或者`nums2[i]`大于`nums1`的最后一项，那就直接push`nums2[i]`到`nums1`最后；另一方面，记住flag的位置，下一次直接从这里开始查找插入新的`nums2[i]`的位置。

暂时没有比较优秀的解答，提升的双指针法也没想到怎么用。







































