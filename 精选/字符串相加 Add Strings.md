### 字符串相加 Add Strings 

#### 题目

给定两个字符串形式的非负整数 `num1` 和`num2` ，计算它们的和。 

**注意：**

1. `num1` 和`num2` 的长度都小于 5100.
2. `num1` 和`num2` 都只包含数字 `0-9`.
3. `num1` 和`num2` 都不包含任何前导零。
4. *你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式。*

#### 解答

思路1： 这道题明确了不让直接将字符串转为数字来计算，乍一看好像有点变态，实际上是考虑到了整型溢出的问题，超出`Number.MAX_SAFE_INTEGER`的数字进行计算已经没有意义了。所以题目中提到了字符串的长度可能在5000左右。这样的话就只能手动计算了，每次取`num1`和`num2`的最后一位进行计算，记录进的位数，然后不断拼接字符串，有点像手写加法计算。

```javascript
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */
var addStrings = function(num1, num2) {
  var len1 = num1.length, len2 = num2.length;
  var len = Math.max(len1, len2), sum = '', x = 0, y = 0, flag = 0;
  for(var i = 0; i < len; i++){
    x = num1[len1-1-i] ? +num1[len1-1-i] : 0;
    y = num2[len2-1-i] ? +num2[len2-1-i] : 0;
    sum = (x + y + flag) % 10 + sum;
    flag = parseInt((x+y+flag) / 10);
  }
  return flag === 0 ? sum : flag+sum;
};
```

提交通过，基本上优秀的解答都是这个思路，感觉还可以。