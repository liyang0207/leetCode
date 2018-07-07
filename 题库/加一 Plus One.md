### 加一 Plus One

### 题目

给定一个**非负整数**组成的**非空**数组，在该数的基础上加一，返回一个新的数组。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

示例：

```javascript
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。

输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
```

标签： `数组` `数学`

### 解答

思路1：这道题很多人点“反对”，我猜应该是题目的中文翻译太烂，初读一遍根本不知道在说什么。初看这道题，想着不就是直接将数组`join`成字符串，转数字再加一，然后再`split`回去。问题来了：首先`split`回去类型是字符串，不是数字，错；其次这道题有一个坑，就是整型溢出的情况，`join`成字符串转数字可能会溢出，溢出之后计算就已经不准确了；还有就是要考虑`[9]`,`[9,9]`这种情况，首项要`unshift`个1。

```javascript
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
  for(var i = digits.length - 1; i > -1; i--){
    if(digits[i] + 1 === 10){
      digits[i] = 0;
      if(!digits[i-1]){
        digits.unshift(1);
        break;
      }
    } else {
      digits[i] += 1;break;
    }
  }
  return digits;
};
```

基本思路是对的，就是解答不够简洁，整理一下。

思路2：整理代码逻辑，简化。

```javascript
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
  for(var i = digits.length - 1; i > -1; i--){
    if(digits[i] < 9){
      digits[i]++;
      return digits;
    }
    digits[i] = 0;
  }
  return [1, ...digits];
};
```

相比于思路1，这里代码更加简洁易懂，用到了`ES6`的`...`运算符，也可以使用`concat`或者`unshift`。