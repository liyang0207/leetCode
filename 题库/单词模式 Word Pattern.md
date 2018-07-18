### 单词模式 Word Pattern 

#### 题目

给定一种 `pattern(模式)` 和一个字符串 `str` ，判断 `str` 是否遵循相同的模式。

这里的**遵循**指完全匹配，例如， `pattern` 里的每个字母和字符串 `str` 中的每个非空单词之间存在着双向连接的对应模式。

示例：

```javascript
输入: pattern = "abba", str = "dog cat cat dog"
输出: true

输入:pattern = "abba", str = "dog cat cat fish"
输出: false

输入: pattern = "aaaa", str = "dog cat cat dog"
输出: false

输入: pattern = "abba", str = "dog dog dog dog"
输出: false
```

**说明:** 你可以假设 `pattern` 只包含小写字母， `str` 包含了由单个空格分隔的小写字母。     

标签： `哈希表`

#### 解答

思路1：这道题难点在与跟以往的js对象思维不同，这道题目要想一个map表通过，必须得是key和value都不能重复的map对象才行。貌似js无法简单实现，这里就直接两个map表相互检验，一个`key-value`、一个`value-key`，双重验证才行。

```javascript
/**
 * @param {string} pattern
 * @param {string} str
 * @return {boolean}
 */
var wordPattern = function(pattern, str) {
  var map1 = {}, map2 = {};
  var arr1 = pattern.split(''), arr2 = str.split(' ');
  if(arr1.length !== arr2.length) return false;
  for(var i = 0; i < arr1.length; i++){
    if(map1[arr1[i]] && map1[arr1[i]] !== arr2[i]) return false;
    if(map2[arr2[i]] && map2[arr2[i]] !== arr1[i]) return false;
    map1[arr1[i]] = arr2[i];
    map2[arr2[i]] = arr1[i];
  }
  return true;
};
```

提交测试通过。







