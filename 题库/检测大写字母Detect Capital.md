### 检测大写字母Detect Capital

#### 题目

给定一个单词，你需要判断单词的大写使用是否正确。

我们定义，在以下情况时，单词的大写用法是正确的：

1. 全部字母都是大写，比如"USA"。
2. 单词中所有字母都不是大写，比如"leetcode"。
3. 如果单词不只含有一个字母，只有首字母大写， 比如 "Google"。

否则，我们定义这个单词没有正确使用大写字母。

示例：

```javascript
输入: "USA"
输出: True

输入: "FlaG"
输出: False
```

**注意:** 输入是由大写和小写拉丁字母组成的非空单词。

#### 解答

思路1：先循环字符串，将字符串内的大写字母数量统计出来（根据charCodeAt()判断字符的Unicode值，小于91的字母都是大写），然后再根据大写字母的数量来进行判断。

```javascript
/**
 * @param {string} word
 * @return {boolean}
 */
var detectCapitalUse = function(word) {
  var num = 0, len = word.length;
  for(var i = 0; i < len; i++){
    if(word.charCodeAt(i) < 91){
      num++;
    }
  }
  if(num === 0 || num === len) return true;
  if(num === 1 && word.charCodeAt(0) < 91) return true;
  return false;
};
```

提交通过。