### 反转字符串II Reverse String II

#### 题目

给定一个字符串和一个整数 k，你需要对从字符串开头算起的每个 2k 个字符的前k个字符进行反转。如果剩余少于 k 个字符，则将剩余的所有全部反转。如果有小于 2k 但大于或等于 k 个字符，则反转前 k 个字符，并将剩余的字符保持原样。

示例：

```javascript
输入: s = "abcdefg", k = 2
输出: "bacdfeg"
```

**要求:**

1. 该字符串只包含小写的英文字母。
2. 给定字符串的长度和 k 在[1, 10000]范围内。

#### 解答

思路1：现将字符串转为数组，在数组长度大于`k`的时候while循环，每次循环取`2k`长度，前`k`项反转，剩下`k`(或小于`k`)的项继续拼接到末尾。

```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var reverseStr = function(s, k) {
  var len = s.length, str = '', arr = s.split('');
  while(arr.length > k){
    var temp = arr.splice(0, 2*k);
    str += (temp.splice(0, k).reverse().join('') + temp.join(''));
  }
  str += arr.reverse().join('');
  return str;
};
```

提交通过。