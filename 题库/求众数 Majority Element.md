### 求众数 Majority Element

#### 题目

给定一个大小为 *n* 的数组，找到其中的众数。众数是指在数组中出现次数**大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

示例：

```javascript
输入: [3,2,3]
输出: 3

输入: [2,2,1,1,1,2,2]
输出: 2
```

标签： `数组`  `位运算` `分治算法`

#### 解答

思路1： 建立map表，循环记录每个值出现的次数，当次数大于`n/2`的时候，将该值返回

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
  var map = {};
  var len = nums.length;
  var cur;
  var max = Math.floor(len / 2);
  for(var i = 0; i < len; i++){
    cur = nums[i];
    if(!map[cur]){
      map[cur] = 0;
    }
    map[cur] += 1;
    if(map[cur] > max){
      return cur;
    }
  }
};
```

提交通过，感觉方法还可以。