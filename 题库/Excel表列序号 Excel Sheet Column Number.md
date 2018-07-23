### Excel表列序号 Excel Sheet Column Number 

#### 题目

给定一个Excel表格中的列名称，返回其相应的列序号。 

示例：

```javascript
输入: "A"
输出: 1

输入: "AB"
输出: 28

输入: "ZY"
输出: 701
```

标签：`数学`

#### 解答

思路1： 每一个字母依据其位置和“大小”的不同，对应不同的值。类似于数字`1234`，可以看成`1*1000 + 2*100 + 3*10 + 4*1`组合而成的，依据这个规律，来解这道题。

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var titleToNumber = function(s) {
  var map = {A: 1, B:2, C:3, D:4, E:5, F: 6, G:7, H: 8, I:9, J:10, K:11, L:12, M: 13, N:14, O: 15, P:16, Q:17, R:18, S:19, T: 20, U:21, V: 22, W:23, X:24, Y:25, Z:26};
  var len = s.length, result = 0;
  for(var i = 0; i < len; i++){
    result += Math.pow(26, len-1-i) * map[s[i]];
  }
  return result;
};
```

提交通过。简单来说，`ABC`可以看做是`1*26*26 + 2*26 + 3*1`组成。

思路2：其实思路1的map表可以使用`Unicode`编码表来代替，使用`string.charCodeAt(i)`来取字母对应的数值。

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var titleToNumber = function (s) {
  var result = 0, len = s.length
  for (let i = 0; i < len; i++) {
    result += (s[i].charCodeAt(0) - 64) * (Math.pow(26, len - 1 - i))
  }
  return result;
};
```

提交通过，整体来看代码更加简洁，省去了map的建立。但是性能貌似不如建立好的map表。

