### 存在重复元素 Contains Duplicate 

#### 题目

给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

示例：

```javascript
输入: [1,2,3,1]
输出: true

输入: [1,2,3,4]
输出: false

输入: [1,1,1,3,3,4,3,2,4,2]
输出: true
```

标签： `数组` `哈希表`

### 解答

思路1：建立map表，循环记录元素出现的次数，当次数为2的时候，直接`return true`，否则`return false`。

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
  var map = {},len = nums.length, cur;
  for(var i = 0; i < len; i++){
    cur = nums[i];
    if(!map[cur]){
      map[cur] = 0;
    }
    map[cur] += 1;
    if(map[cur] === 2){
      return true;
    }
  }
  return false;
};
```

提交通过，查看优秀答案，发现另外一个比较好的思路。

思路2：利用`Set`元素不能重复的特性，将数组转为`Set`，再比较`set.size`和原数组的长度，变短了则说明有重复的元素。

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
  var set = new Set(nums);
  return set.size !== nums.length;
};
```

这个解答还是很不错的，充分利用了`ES6`的特性，简单又巧妙。



