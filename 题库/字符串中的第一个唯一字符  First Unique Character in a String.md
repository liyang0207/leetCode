### 字符串中的第一个唯一字符  First Unique Character in a String

#### 题目

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。 

示例：

```javascript
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
```

**注意事项：**您可以假定该字符串只包含小写字母 

`字符串` `哈希表`

#### 解答

思路1：一层循环，建立map表来储存字符串中出现两次及以上的字符，碰到没有出现两次的字符，返回。

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var firstUniqChar = function(s) {
  var map = {};
  for(var i = 0; i < s.length; i++){
    if(map[s[i]]) continue;
    if(s.indexOf(s[i], i+1) < 0){
      return i;
    }else{
      map[s[i]] = true;
    }
  }
  return -1;
};
```

提交通过，查看优秀解答，发现一个思路，分别从头和从尾开始查找一个字符，如果两者返回的index一致，则说明是出现一次的字符，又因为从前到后循环，第一次满足条件的就是第一个。

思路2： 使用`lastIndexOf`判断。

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var firstUniqChar = function(s) {
    var len = s.length;
    for (var i = 0; i < len; i++) {
        if (s.indexOf(s[i]) === i && s.lastIndexOf(s[i]) === i) {
            return i
        }
    }
    return -1;
};
```

这个思路很不错。
