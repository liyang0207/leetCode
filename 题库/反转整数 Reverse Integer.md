### 反转整数 Reverse Integer

#### 题目

给定一个 32 位有符号整数，将整数中的数字进行反转。 

示例：

```javascript
输入: 123
输出: 321

输入: -123
输出: -321

输入: 120
输出: 21
```

注意：假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−2^31,  2^31 − 1]。根据这个假设，如果反转后的整数溢出，则返回 0。 

标签： `数学`

#### 解答

思路1：初次思考该题时，思维限定到了“有符号”的整数，以为符号除了`+` `-`之外还会有其他；另外一个要注意的点是末尾的0反转之后需要裁剪掉；说到反转就想到了数组的`reverse()`方法。

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
  var result;
  var arr = x.toString().split('');
  var mark = (/^\d/).test(arr[0]) ? '' : arr.splice(0, 1);
  var temp = arr.reverse();
  while (temp.indexOf('0') == 0) {
    temp.splice(0, 1);
  }
  result = +(mark + temp.join(''));
  if (result < - Math.pow(2, 31) || result > (Math.pow(2, 31) - 1)) {
    return 0;
  }
  return result;
};
```

提交通过，测试用时136ms，	大概排提交答案速度的前17.33%，方法看起来很粗糙，效率低下。查看优秀解答之后发现，符号这边只需要判断正负即可，不需要单独`splice()`出来最后再拼接；对于反转之后首位0处理也不需要使用`while`循环，`+'0123'`直接隐式转换为数字`123`；不过最重要的提升还是在于反转的数学方式将值`弹出`和`推入`，使用取余和取整，注意观察这种技巧。

思路2：舍去多余的操作动作，使用数学方式反转数字，减少操作过程。

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
  var mark = x > 0 ? 1 : -1;
  var reverseNum = 0;
  var num = Math.abs(x);
  while (num > 0) {
    reverseNum = reverseNum * 10 + num % 10;
    num = parseInt(num/10);
  }
  if ( reverseNum > Math.pow(2, 31) - 1) { return 0; }
  return reverseNum * mark;
};
```

加入输入1234，注意观察`reverseNum`，循环过程中依次为4，43，432，4321，使用数学取余和取整来进行反转整数。