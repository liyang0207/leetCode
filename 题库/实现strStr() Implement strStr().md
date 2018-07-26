### 实现strStr() Implement strStr() 

#### 题目

实现 [strStr()](https://baike.baidu.com/item/strstr/811469) 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  **-1**。

示例：

```javascript
输入: haystack = "hello", needle = "ll"
输出: 2

输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

标签： `双指针` `字符串`

**说明:**

当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 `needle` 是空字符串时我们应当返回 0 。这与C语言的 [strstr()](https://baike.baidu.com/item/strstr/811469) 以及 Java的 [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)) 定义相符。

#### 解答

思路1： 循环`haystack`，先找到值为`needle[0]`的位置，然后截取之后`nlen`的长度对比。

```javascript
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
  if(needle === '') return 0;
  var hlen = haystack.length, nlen = needle.length;
  for(var i = 0; i < hlen - nlen + 1; i++){
    if(haystack[i] === needle[0]){
      if(haystack.substr(i, nlen) === needle) return i;
    }
  }
  return -1;
};
```

提交通过，但是查看答案发现很多人直接使用`indexOf()`，明显与题意不符，搞不懂。







