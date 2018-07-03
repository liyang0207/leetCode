### 回文数 Palindrome Number

#### 题目

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。 

示例：

```javascript
输入: 121
输出: true

输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```

标签：`数学`

### 解答

思路1：刚开始思考的时候又想到了-0的情况，不过貌似leetCode上的题目都忽略了-0，故直接不考虑这种情况；负整数肯定返回false，直接`return false`；回文肯定又要反转整数，之前遇到过的`Reverse Integer`题目中的取余取整的方法直接拿来实践一下；

```javascript
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
  if (x < 0) { return false; }
  var reverseNum = 0, source = x;
  while (x > 0) {
    reverseNum = reverseNum * 10 + x % 10;
    x = parseInt(x/10);
  }
  if (source === reverseNum) {
    return true;
  }
  return false;
};
```

提交测试通过，但不是最优的解。好像使用测试用时来判断答案的优劣是不靠谱的，同一个方法提交测试时间有时候会差很多，我们就直接看一些最优解的思路。这个题目优化的地方有二：1.末尾数是0的必然无法通过，那就直接通过取余数来过滤掉这种情况；2.反转的时候可以只反转一半的数字，一来节省计算时间，二来可以避免整数溢出的问题，反转一半的节点在`x`小于等于`reverseNum`的时候，对于偶数，循环停止时`x`位数等于`reverseNum`；对于奇数，循环停止时`reverseNum`位数比`x`多一位，但多的这一位正好是中间值，相当于两者共用，那就直接判断`parseInt(reverseNum/10)`是否与`x`相等即可。

思路2：直接排除负整数和10的倍数；循环反转整数的时候只反转一半，处理好停止循环的节点即可。

```javascript
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
  if (x < 0 || (x !== 0 && x % 10 === 0)) {
    return false;
  }
  var reverseNum = 0;
  while (x > reverseNum) {
    reverseNum = reverseNum * 10 + x % 10;
    x = parseInt(x / 10);
  }
  return x === reverseNum || x === parseInt(reverseNum / 10);
};
```

测试通过，测试用时还是很久，所以觉得这个测试用时还是不太靠谱（使用leetCode中文版的原因？）。总结一下，自以为自己掌握了反转整数的方法，却不知道只掌握了死方法，没有更加灵活的使用；同时没有深入思考整数末尾是0的情况；反转的时候没有考虑到整数溢出的i情况；还是需要多多思考。
