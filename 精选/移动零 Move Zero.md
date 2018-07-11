### 移动零  Move Zero

#### 题目

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。  

示例：

```javascript
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```

说明：必须在原数组上操作，不能拷贝额外的数组，尽量减少操作次数 。

标签： `数组` `双指针`

#### 解答

思路1：循环的次数必须小于数组长度，使用一个变量来表示记录循环次数。每次循环找到为0的项，将其剪切，然后添加到队尾。

```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var moveZeroes = function(nums) {
  var j = 0, len = nums.length;
  for(var i = j; i < len; i++){
    if(j === len){
      break;
    }
    if(nums[i] === 0){
      nums.splice(i, 1);
      nums.push(0);
      i--;
    }
    j++;
  }
};
```

提交通过，但感觉很乱。需简化。

思路2：重点在于记录循环次数和操作数组，下面的方法很巧妙。

```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var moveZeroes = function(nums) {
  var len = nums.length;
  for(var i = 0; i < len; i++){
    if(nums[i] === 0){
      nums.splice(i--, 1);
      nums.push(0);
      len--;
    }
  }
};
```

每次遇到0的时候就将`len`减少1位数，同时要注意`nums.splice(i--, 1)`是先剪切，再将`i`减掉1，这个要注意。