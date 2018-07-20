### 键盘行 Keyboard Row 

#### 题目

给定一个单词列表，只返回可以使用在键盘同一行的字母打印出来的单词。键盘如下图所示。 

示例：

```javascript
输入: ["Hello", "Alaska", "Dad", "Peace"]
输出: ["Alaska", "Dad"]
```

**注意:**

1. 你可以重复使用键盘上同一字符。
2. 你可以假设输入的字符串将只包含字母。

标签： `哈希表`

#### 解答

思路1： 键盘每行字都是固定的，建立3个map表，对于每一个字符串，先判断第一个字符确定第几行的，然后在该行map循环，判断该字符是否全部在这一行。

```javascript
/**
 * @param {string[]} words
 * @return {string[]}
 */
var findWords = function(words) {
  var arr1 = ['q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'],
      arr2 = ['a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'],
      arr3 = ['z', 'x', 'c', 'v', 'b', 'n', 'm'];
  var result = [], flag = false, target;
  for(var i = 0; i < words.length; i++){
    var cur = words[i][0].toLowerCase();
    if(arr1.indexOf(cur) > -1){
      target = arr1;
    }else if(arr2.indexOf(cur) > -1){
      target = arr2;
    }else{
      target = arr3;
    }
    flag = words[i].split('').every((word) => {
      return target.indexOf(word.toLowerCase()) > -1;
    })
    flag ? result.push(words[i]) : '';
  }
  return result;
};
```

提交通过，但是很繁琐。查看优秀解答，发现原来可以使用正则匹配，这才是比较好的解法。

思路2： 使用正则来解该题，简单优雅。

```javascript
/**
 * @param {string[]} words
 * @return {string[]}
 */
var findWords = function(words) {
    // 真正优秀的解答
    let r = /^([qwertyuiop]*|[asdfghjkl]*|[zxcvbnm]*)$/i,
        result=[];
    words.forEach(val=>{
        if(r.test(val)) result.push(val)
    })
    return result;
};
```

`i`不区分大小写，对于此题在适合不过了。





