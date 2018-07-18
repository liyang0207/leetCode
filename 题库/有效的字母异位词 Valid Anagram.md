### 有效的字母异位词 Valid Anagram 

#### 题目

给定两个字符串 *s* 和 *t* ，编写一个函数来判断 *t* 是否是 *s* 的一个字母异位词。 

示例：

```javascript
输入: s = "anagram", t = "nagaram"
输出: true 

输入: s = "rat", t = "car"
输出: false
```

**说明:**
你可以假设字符串只包含小写字母。

**进阶:**
如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？

标签： `排序` `哈希表`

#### 解答

思路1：建立map 表，但是单单将第一个值存入map表，然后判断另外一个值的给项是否存在与这个map中还不行，得考虑到字符出现次数的问题，所以map表中存入各字符出现的次数，然后第二次循环来判断第二个值出现的次数是否一致。

```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
  if(s.length !== t.length) return false;
  var map = {};
  for(var i = 0; i<s.length; i++){
    if(map[s[i]] != null){
      map[s[i]]++;
    }else {
      map[s[i]] = 1;
    }
  }
  for(var j = 0; j < t.length; j++){
    if(map[t[j]] != null){
      map[t[j]]--;
      if(map[t[j]] < 0){
        return false;
      }
    }else{
      return false;
    }
  }
  return true;
};
```

提交测试通过，感觉js在应对哈希表类型题目的时候比较吃力 。







