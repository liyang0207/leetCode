### 缺失数字 Missing Number

#### 题目

给定一个包含 `0, 1, 2, ..., n` 中 *n* 个数的序列，找出 0 .. *n* 中没有出现在序列中的那个数。 

示例：

```javascript
输入: [3,0,1]
输出: 2

输入: [9,6,4,2,3,5,7,0,1]
输出: 8
```

标签： `数组` `位运算` `数学`

#### 解答

思路1：将数组先排序，然后循环找到项不等于`i`的那一项，返回`i`值就是。不过要注意循环次数等于数组长度。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
    nums.sort((a, b) => {
      return a - b;
    })
  for(var i = 0; i <= nums.length; i++){
    if(nums[i] !== i){
      return i;
    }
  }
};
```

提交通过，但是速度不够快，性能不好，多了一步排序。

思路2：数组和与`1+2+...+n`的差值就是目标值。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
    var sum = 0;
    var k = nums.length;
    for(var i=0;i<nums.length;i++){
        sum  = sum + nums[i];
    }
    var k = nums.length;
    return ((k*(k+1))/2)-sum; 
};
```

需要知道`1+2+...+n`的求和公式：`k*(k+1))/2`