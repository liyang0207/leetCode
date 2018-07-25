### 完美数 Perfect Number

#### 题目

------

对于一个 **正整数**，如果它和除了它自身以外的所有正因子之和相等，我们称它为“完美数”。

给定一个 **正整数** `n`， 如果他是完美数，返回 `True`，否则返回 `False`

示例：

```javascript
输入: 28
输出: True
解释: 28 = 1 + 2 + 4 + 7 + 14
```

**注意:** 输入的数字 **n** 不会超过 100,000,000. (1e8)

标签： `数学`

#### 解答

思路1： 从1开始递增循环，判断`n`对`i`取余是否为0，然后每次都修正循环的最大值，将结果push到结果集中，求和。

```javascript
/**
 * @param {number} num
 * @return {boolean}
 */
var checkPerfectNumber = function(num) {
  var arr = [], flag = num, sum = 1;
  if(num === 1) return false;
  for(var i = 2; i < flag; i++){
    if((num % i) === 0){
      arr.push(i);
      arr.push(num/i)
      flag = num/i;
    }
  }
  for(var j = 0; j < arr.length; j++){
    sum = sum + arr[j];
  }
  return sum === num;
};
```

提交通过，需要优化。每次循环貌似可以直接求和。

思路2： 循环时就求和。

```javascript
/**
 * @param {number} num
 * @return {boolean}
 */
var checkPerfectNumber = function(num) {
  if (num <= 1) return false;
  var sum = 1;
  for (var i = 2; i <= Math.sqrt(num); i++) {
    if(num % i === 0) {
      sum += i;
      if (num / i !== i) {
        sum += num / i;
      }
    }
  }
  return num === sum;
};
```

一次循环，循环的时候就求和，然后循环最大值为num的开平方。

