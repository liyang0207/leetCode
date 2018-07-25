### 平方数之和 Sum of Square Numbers 

#### 题目

 给定一个非负整数 `c` ，你要判断是否存在两个整数 `a` 和 `b`，使得 a2 + b2 = c。 

示例：

```javascript
输入: 5
输出: True
解释: 1 * 1 + 2 * 2 = 5

输入: 3
输出: False
```

标签： `数学`

#### 解答

思路1： 这里需要注意的一点是`a`和`b`可能相等。建立map表，循环的时候看看`c - i*i`是否在map表内，在就输出`true`。

```javascript
/**
 * @param {number} c
 * @return {boolean}
 */
var judgeSquareSum = function(c) {
  var map = {}, cur = 0;
  for(var i = 0; i <= Math.sqrt(c); i++){
    cur = i*i;
    map[cur] = i;
    if(map[c-cur] != null){
      return true;
    }
  }
  return false;
};
```

提交通过，简化一下。

思路2： 直接判断`cur - i*i`的开平方是否为整数即可。

```javascript
/**
 * @param {number} c
 * @return {boolean}
 */
var judgeSquareSum = function(c) {
  for(var i = 0; i <= Math.sqrt(c); i++){
    if(Number.isInteger(Math.sqrt(c - i*i))) return true;
  }
  return false;
};
```

简单明了。

