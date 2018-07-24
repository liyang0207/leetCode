### 排列硬币 Arranging Coins 

#### 题目

你总共有 *n* 枚硬币，你需要将它们摆成一个阶梯形状，第 *k* 行就必须正好有 *k* 枚硬币。

给定一个数字 *n*，找出可形成完整阶梯行的总行数。

*n* 是一个非负整数，并且在32位有符号整型的范围内。

示例：

```javascript
n = 5

硬币可排列成以下几行:
¤
¤ ¤
¤ ¤

因为第三行不完整，所以返回2.

n = 8

硬币可排列成以下几行:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

因为第四行不完整，所以返回3.
```



#### 解答

思路1： 感觉这道题的思路很清晰，就是不断累加硬币数，`1+2+3+4+...`，直到总数大于`n`的时候停止，然后返回`i`值就好，剩下的就是细节处理了。

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var arrangeCoins = function(n) {
  var result = 0, i = 1;
  if(n < 2) return n;
  while(n > result){
    result += i;
    if(result === n) return i;
    i++;
  }
  return i-2;
};
```

提交通过，但是感觉假动作太多，应该可以精简一下。

思路2： 精简代码。

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var arrangeCoins = function(n) {
  var sum = 0, i = 0;
  while(sum <= n){
    sum = sum + ++i;
  }
  return (i-1);
};
```







