### 反转字符串中的元音字母 Reverse Vowels of a String 

#### 题目

编写一个函数，以字符串作为输入，反转该字符串中的元音字母。 

示例：

```javascript
给定 s = "hello", 返回 "holle".
给定 s = "leetcode", 返回 "leotcede".
```

**注意:** 元音字母不包括 "y". 

#### 解答

思路1： 题目有点难懂，反转元音字母的意思是第一个元音字母跟最后一个元音字母对调位置，这样来说就必须循环完整个字符串，找到所有的元音字母后才能反转。不过看到字符串的操作，第一时间可以想到正则表达式，使用`match()`来取出来所有的元音字母，存入数组，要注意如果没有匹配到任何值，会返回`null`。这之后就是很正常的循环字符串，反转字母了，不过我们是无法直接操作字符串的。

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var reverseVowels = function(s) {
  var arr = s.match(/[aeiou]/gi), result = '', len = arr ? arr.length : 0, flag = 0;
  for(var i = 0; i < s.length; i++){
    if((/[aeiou]/gi).test(s[i])){
      result += arr[len-flag-1];
      flag++;
    }else{
      result += s[i];
    }
  }
  return result;
};
```

提交通过。总体来看思路比较清晰，简单明了。