### 反转字符串中的单词 III Reverse Words in a String III

#### 题目

给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

 示例：

```javascript
输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc" 
```

**注意：**在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。

#### 解答

思路1： 直接将字符串转为数组进行反转拼接操作。

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {
  return s.split(' ').map(str => {
    return str.split('').reverse().join('');
  }).join(' ');
};
```

提交通过，不过这道题如果使用`forEach`的话要注意，`forEach`没有返回值。