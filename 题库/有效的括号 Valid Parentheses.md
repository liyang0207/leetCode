### 有效的括号 Valid Parentheses

#### 题目

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串，判断字符串是否有效。 

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

示例：

```javascript
输入: "()"
输出: true

输入: "()[]{}"
输出: true

输入: "(]"
输出: false

输入: "([)]"
输出: false

输入: "{[]}"
输出: true
```

标签： `栈` `字符串`

#### 解答

思路1：题目有一种入栈出栈的感觉，用数组来模拟栈；建立map表，将括号转为能抵消的正负数；循环字符串，不断的入栈出栈，最后判断栈的长度；写到这里突然想到循环可以提前结束，节省时间；

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
  const map = {
    '(': 1,
    ')': -1,
    '{': 2,
    '}': -2,
    '[': 3,
    ']': -3
  }
  var arr = s.split('');
  var result = [];
  for (let i = 0; i < arr.length; i++) {
    if (map[result[result.length - 1]] + map[arr[i]] === 0) {
      result.pop();
    } else {
      result.push(arr[i]);
    }
  }
  return result.length === 0;
};
```

这个是测试通过的版本，时间可以，想到上面提到可以提前结束循环，想到一个优化的地方，写到思路2。

思路2：思路1的基础上，提前结束循环，每次循环结束后判断最后一位是不是`)` `}` `]`中的任一，是则提前结束循环。

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
  const map = {
    '(': 1,
    ')': -1,
    '{': 2,
    '}': -2,
    '[': 3,
    ']': -3
  }
  var arr = s.split('');
  var result = [];
  for (let i = 0; i < arr.length; i++) {
    if (map[result[result.length - 1]] + map[arr[i]] === 0) {
      result.pop();
    } else {
      result.push(arr[i]);
    }
    if (map[result[result.length - 1]] < 0) { break; }
  }
  return result.length === 0;
};
```

提交通过，但是这里发现一种情况测试没有测出来，即')))((('的情况，我的第一个解答可以通过官网验证，而且对这种情况返回了true(应该为false)。故第一种方法不严谨。已为社区提交测试用例。