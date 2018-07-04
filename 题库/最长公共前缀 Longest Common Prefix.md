### 最长公共前缀 Longest Common Prefix

#### 题目

编写一个函数来查找字符串数组中的最长公共前缀。如果不存在公共前缀，返回空字符串 `""`。

示例：

```
输入: ["flower","flow","flight"]
输出: "fl"

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
```

说明：所有输入只包含小写字母 `a-z` 。 

标签： `字符串`

#### 解答

思路1：只有小写字母，需要考虑空数组，返回空字符串，只有1个元素的数组应该返回自己；循环应该最少一次，考虑使用`every`方法，通过返回true或false来提前结束`for`循环；将第一个元素作为基准，前缀每次叠加一位；

```javascript
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function(strs) {
  var temp, first = strs[0], prefix = '', result = '';
  if (strs.length === 0) { return '';}
  for (var i = 0; i < first.length; i++) {
    prefix += first[i];
    temp = strs.every(function(str){
      return str.indexOf(prefix) === 0;
    })
    if(!temp) { break; }
    result = prefix;
  }
  return result;
};
```

提交测试通过，用时还可以。其他解答暂时没有发现让人眼前一亮的解答，这个解答看起来还不错~

