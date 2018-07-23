### 2的幂 Power of Two 

#### 题目

给定一个整数，编写一个函数来判断它是否是 2 的幂次方。 

示例：

```javascript
输入: 1
输出: true
解释: 20 = 1

输入: 16
输出: true
解释: 24 = 16

输入: 218
输出: false
```

标签：`数学`

#### 解答

思路1： 不断循环，直到等于`2`的`i`次幂，或者大于`n`。

```javascript
/**
 * @param {number} n
 * @return {boolean}
 */
var isPowerOfTwo = function(n) {
  var result = 0, i = 0;
  while(n > result){
    result = Math.pow(2, i)
    if(n === result){
      return true;
    }else{
      i++;
    }
  }
  return false;
};
```

提交通过。

