### 只出现一次的数字 Single Number 

#### 题目

给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

**说明：**

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例：

```javascript
输入: [2,2,1]
输出: 1

输入: [4,1,2,1,2]
输出: 4
```

标签： `位运算` `哈希表`

#### 解答

思路1：没有想到比较简单的方法一步做出来。建立map表，循环数组，如果map中存在，就将该值删去，如果没有就把该值作为map的一个属性，赋值true，最后通过`Object.keys(map)[0]`取出里面的唯一属性。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
  var map = {},len = nums.length, cur;
  for(var i = 0; i < len; i++){
    cur = nums[i];
    if(map[cur] != null){
      delete map[cur];
    }else{
      map[cur] = true;
    }
  }
  return +Object.keys(map)[0];
};
```

提交通过。查看其它解答，几乎都是在使用`^`异或符号来解答，简单是简单，但是js中貌似没有这个运算符吧，搞不懂。

