### 比较含退格的字符串  Backspace String Compare 

#### 题目

给定 `S` 和 `T` 两个字符串，当它们分别被输入到空白的文本编辑器后，判断二者是否相等，并返回结果。 `#` 代表退格字符。 

示例：

```javascript
输入：S = "ab#c", T = "ad#c"
输出：true
解释：S 和 T 都会变成 “ac”。

输入：S = "ab##", T = "c#d#"
输出：true
解释：S 和 T 都会变成 “”。

输入：S = "a##c", T = "#a#c"
输出：true
解释：S 和 T 都会变成 “c”。

输入：S = "a#c", T = "b"
输出：false
解释：S 会变成 “c”，但 T 仍然是 “b”。
```

**提示：**

1. `1 <= S.length <= 200`
2. `1 <= T.length <= 200`
3. `S` 和 `T` 只含有小写字母以及字符 `'#'`。

标签： `栈` `双指针`

#### 解答

思路1： 栈的概念，遇到`#`的就将栈的最后一位弹出，js可以使用数组来模拟栈的概念。分别循环`S`和`T`，最后对比两个栈即可。

```javascript
/**
 * @param {string} S
 * @param {string} T
 * @return {boolean}
 */
var backspaceCompare = function(S, T) {
  var arr1 = [], arr2 = [];
  for(var i = 0; i < S.length; i++){
    S[i] === '#' ? arr1.pop() : arr1.push(S[i]);
  }
  for(var j = 0; j < T.length; j++){
    T[j] === '#' ? arr2.pop() : arr2.push(T[j]);
  }
  return arr1.join('') === arr2.join('');
};
```

提交通过。其实最后的`join('')`中的`''`可以省略。