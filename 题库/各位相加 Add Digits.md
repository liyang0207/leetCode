### 各位相加 Add Digits 

#### 题目

给定一个非负整数 `num`，反复将各个位上的数字相加，直到结果为一位数。 

示例：

```javascript
输入: 38
输出: 2 
解释: 各位相加的过程为：3 + 8 = 11, 1 + 1 = 2。 由于 2 是一位数，所以返回 2。
```

**进阶:** 你可以不使用循环或者递归，且在 O(1) 时间复杂度内解决这个问题吗？ 

标签：`数学`

#### 解答

思路1：循环相加，return最后值。

```javascript
/**
 * @param {number} num
 * @return {number}
 */
var addDigits = function(num) {
  var temp;
  while(num > 9){
    temp = 0;
    while(num > 0){
      temp = temp + num % 10;
      num =parseInt(num/10);
    }
    num = temp;
  }
  return num;
};
```

提交通过。优秀解答有种解答方式不是很懂。

思路2：优秀解答

```javascript
/**
 * @param {number} num
 * @return {number}
 */
var addDigits = function (num) {
    return (num-1) % 9+1;
};
```

不是很懂。