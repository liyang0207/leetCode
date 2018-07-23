### Excel表列名称 Excel Sheet Column Title 

#### 题目

给定一个正整数，返回它在 Excel 表中相对应的列名称。 

示例：

```javascript
输入: 1
输出: "A"

输入: 28
输出: "AB"

输入: 701
输出: "ZY"
```

标签：`数学`

#### 解答

思路1： 26个英文字母，每26进一位，有点像26进制的感觉，每次就对26取余数，然后借助字母map数组填充字母。这个数组也类似于对象，即`index->value`。

```javascript
/**
 * @param {number} n
 * @return {string}
 */
var convertToTitle = function(n) {
  var map = ['Z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y'];
  var result = '';
  while(n > 0){
    result = map[n % 26] + result;
    n = parseInt((n-1)/26);
  }
  return result;
};
```

提交通过。

