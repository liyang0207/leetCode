### 找不同 Find the Difference 

#### 题目

给定两个字符串 **s** 和 **t**，它们只包含小写字母。字符串 **t** 由字符串 **s** 随机重排，然后在随机位置添加一个字母。请找出在 **t** 中被添加的字母。 

示例：

```javascript
输入：
s = "abcd"
t = "abcde"

输出：
e

解释：
'e' 是那个被添加的字母。
```

`位运算` `哈希表`

#### 解答

思路1：将字符`s`各项及数量存入map表，循环`t`的时候注意有一个坑，就是假如`s='ccc'`， `t='cccc'`，那么最后返回应该是`c`，所以单纯的循环`t`判断`t`的某一项在不在map表中，就会出问题，所以需要判断数量。这里当`map[t[j]]`不存在或者为`0`的时候，刚好就是结果值。

```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {character}
 */
var findTheDifference = function(s, t) {
  var map = {};
  for(var i = 0; i < s.length; i++){
    if(!map[s[i]]){
      map[s[i]] = 1;      
    }else{
      map[s[i]]++;
    }
  }
  for(var j = 0; j < t.length; j++){
    if(!map[t[j]]){
      return t[j]
    }else{
      map[t[j]]--;
    }
  }
};
```

提交通过。