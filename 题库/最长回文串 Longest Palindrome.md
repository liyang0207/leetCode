### 最长回文串 Longest Palindrome  

#### 题目

给定一个包含大写字母和小写字母的字符串，找到通过这些字母构造成的最长的回文串。在构造过程中，请注意区分大小写。比如 `"Aa"` 不能当做一个回文字符串。

示例：

```javascript
输入:
"abccccdd"

输出:
7

解释:
我们可以构造的最长的回文串是"dccaccd", 它的长度是 7。
```

**注意:** 假设字符串的长度不会超过 1010。 

标签：`位运算` `哈希表`

#### 解答

思路1：建立map表，循环表值，如果表值为偶数，则加上，如果为奇数，则需要考虑是`1`还是`大于1`的情况，因为`ccccc`可以只取4个c！

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var longestPalindrome = function(s) {
  var map = {}, result = 0, flag = false;
  for(var i = 0; i < s.length; i++){
    if(map[s[i]] != null){
      map[s[i]]++;
    }else{
      map[s[i]] = 1;
    }
  }
  var keys = Object.keys(map);
  for(var j = 0; j < keys.length; j++){
    console.log(map[keys[j]])
    if(map[keys[j]] % 2 === 0){
      result += map[keys[j]];
    }else{
      if(map[keys[j]] > 2){
        result += (map[keys[j]] - 1);
      }
      flag = true;
    }
  }
  return flag ? ++result : result;
};
```

提交通过。但是感觉有点繁琐，精简一下。

思路2：使用`for in`精简一下，整理一下思路。

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var longestPalindrome = function(s) {
  var map = Object.create(null), result = 0, flag = false;
  for(var i = 0; i < s.length; i++){
    map[s[i]] != null ? map[s[i]]++ : map[s[i]] = 1;
  }
  for(let j in map){
    result += map[j];
    if(map[j] % 2 !== 0){
      result--;
      flag = true;
    }
  }
  return flag ? ++result : result;
};
```

首先使用`Object.create(null)`创建空对象，然后使用`for..in`简化代码。