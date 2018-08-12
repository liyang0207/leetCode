### 转换成小写字母 To Lower Case

#### 题目

实现函数 ToLowerCase()，该函数接收一个字符串参数 str，并将该字符串中的大写字母转换成小写字母，之后返回新的字符串。

#### 解答

思路1：不能使用`toLowerCase()`方法，那就只能从Unicode编码入手了，建立小写字母map表，循环字符串，当字符Unicode编码为`[65, 90]`之间时，加上32就是对应小写字母的编码值。这里可以使用`Array.prototype.map.call()`借用`Array`方法。

```javascript
/**
 * @param {string} str
 * @return {string}
 */
var toLowerCase = function(str) {
  var map = {'97': 'a', '98': 'b', '99': 'c', '100': 'd', '101': 'e', '102': 'f', '103': 'g', '104': 'h', '105': 'i', '106': 'j', '107': 'k', '108': 'l', '109': 'm', '110': 'n', '111': 'o', '112': 'p', '113': 'q', '114': 'r', '115': 's', '116': 't', '117': 'u', '118': 'v', '119': 'w', '120': 'x', '121': 'y', '122': 'z'}
  return Array.prototype.map.call(str, s => {
    var code = s.charCodeAt(0);
    if(code > 64 && code < 91) return map[code+32];
    return s;
  }).join('');
};
```

提交通过。其实之前一直在想既然有`charCodeAt`方法字符转为编码，有没有编码转为字符的呢？查看解答才发现有`String.fromCharCode(num1, num2, ...)`方法。

思路2： 直接使用`String.fromCharCode()`方法。

```javascript
/**
 * @param {string} str
 * @return {string}
 */
var toLowerCase = function(str) {
  return Array.prototype.map.call(str, s => {
    var code = s.charCodeAt(0);
    if(code > 64 && code < 91) return String.fromCharCode(code+32);
    return s;
  }).join('');
};
```

两种思路都进行字符编码范围的判断，目的是排除其他非字母字符的影响。