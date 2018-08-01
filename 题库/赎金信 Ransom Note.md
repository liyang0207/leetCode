### 赎金信 Ransom Note 

#### 题目

给定一个赎金信 (ransom) 字符串和一个杂志(magazine)字符串，判断第一个字符串ransom能不能由第二个字符串magazines里面的字符构成。如果可以构成，返回 true ；否则返回 false。

(题目说明：为了不暴露赎金信字迹，要从杂志上搜索各个需要的字母，组成单词来表达意思。)

示例：

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

**注意：**你可以假设两个字符串均只含有小写字母。

标签： `字符串`

#### 解答

思路1： 建立两个map表，分别将`ransom`和`magazine`字符串中字符出现的次数记录下来，然后拿`ransom`中的字符串比对`magazine`，写法有些繁杂。

```javascript
/**
 * @param {string} ransomNote
 * @param {string} magazine
 * @return {boolean}
 */
var canConstruct = function(ransomNote, magazine) {
  var map1 = {}, map2 = {};
  for(var i = 0; i < ransomNote.length; i++){
    map1[ransomNote[i]] ? map1[ransomNote[i]]++ : map1[ransomNote[i]] = 1;
  }
  for(var j = 0; j < magazine.length; j++){
    map2[magazine[j]] ? map2[magazine[j]]++ : map2[magazine[j]] = 1;
  }
  for(var k in map1){
    if(map2[k] == null) return false;
    if(map1[k] > map2[k]) return false;
  }
  return true;
};
```

提交通过，其实`ransom`中的每一个字符都必须在`magazine`中找到不重复的对应项，查看优秀解答，发现可以通过对比字符串和数组的方式来解决。

思路2：将`magazine`存入数组，循环`ransom`，每循环一个字符就将数组中对应的项设为`undefined`。

```javascript
/**
 * @param {string} ransomNote
 * @param {string} magazine
 * @return {boolean}
 */
var canConstruct = function(ransomNote, magazine) {
  var arr = magazine.split('');
  for(var i = 0; i < ransomNote.length; i++){
    var idx = arr.indexOf(ransomNote[i]);
    if(idx !== -1){
      arr[idx] = undefined;
    }else{
      return false;
    }
  }
  return true;
};
```

提交解答。