### 无重复字符的最长子串  Longest Substring Without Repeating Characters

#### 题目

给定一个字符串，找出不含有重复字符的**最长子串**的长度。

示例：

```javascript
输入: "abcabcbb"
输出: 3 
解释: 无重复字符的最长子串是 "abc"，其长度为 3。

输入: "bbbbb"
输出: 1
解释: 无重复字符的最长子串是 "b"，其长度为 1。

输入: "pwwkew"
输出: 3
解释: 无重复字符的最长子串是 "wke"，其长度为 3。
     请注意，答案必须是一个子串，"pwke" 是一个子序列 而不是子串。
```

#### 解答

思路1：循环数组，使用数组暂存子串，遇到重复的元素，剪切数组，同时记录目前最长的子串长度。

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
  let len = s.length, result = 0, arr = [];
  for (let i = 0; i < len; i++) {
    if (arr.indexOf(s[i]) > -1) {
      result = Math.max(result, arr.length);
      arr = arr.slice(arr.indexOf(s[i])+1);
      arr.push(s[i]);
    } else {
      arr.push(s[i]);
    }
  }
  return Math.max(result, arr.length);
};
```

简化代码：

```javascript
var lengthOfLongestSubstring = function(s) {
    let arr = [], res = 0;
    for(let i = 0; i < s.length; i++){
        let index = arr.indexOf(s[i])
        if( index > -1){
            arr.splice(0,index + 1)
        }
        arr.push(s[i])
        res = Math.max(res, arr.length)
    }
    return res
};
```

思路2：这种思路比较巧妙，利用指针，只记录非重复子串开始的位置，然后每次循环都记录当前最长子串长度。难点在于何时移动指针，即当前字符的索引值小于当前的i值，说明前面出现过这个字符。

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    if (!s.length) return 0;
    var max = 1, flag = 0
    for(var i = 0; i < s.length; i++) {
        var index = s.indexOf(s[i], flag) 
        if (index !== -1 && index < i) flag = index + 1;
        max = Math.max(max, i - flag + 1)
    }
    return max
};
```

