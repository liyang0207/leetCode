###  验证回文字符串 Ⅱ Valid Palindrome II

#### 题目

给定一个非空字符串 `s`，**最多**删除一个字符。判断是否能成为回文字符串。

示例：

```javascript
输入: "aba"
输出: True

输入: "abca"
输出: True
解释: 你可以删除c字符。
```

注意：字符串只包含从 a-z 的小写字母。字符串的最大长度是50000。

#### 解答

思路1：先从头到字符串中间循环，找到那个首尾不相等的位置`i`，然后分两种情况，要么去掉`i`位置的字符后回文，要么去掉`len-i-1`位置的字符后回文，判读这两种情况即可。

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var validPalindrome = function(s) {
  var arr = s.split(''), len = arr.length, flag = null;
  for(var i = 0; i < Math.floor(len/2); i++){
    if(arr[i] !== arr[len-i-1]){
      flag = i;
      break;
    }
  }
  if(flag == null) return true;
  var temp1 = arr.slice();
  temp1.splice(flag, 1);
  var temp2 = arr.slice();
  temp2.splice(len-flag-1, 1);
  return temp1.join('') === temp1.reverse().join('') || temp2.join('') === temp2.reverse().join('');
};
```

提交通过，不过略显繁琐，但是查看优秀答案暂时没发现比较好的答案，等日后再来重写此题。