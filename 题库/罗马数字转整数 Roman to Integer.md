### 罗马数字转整数 Roman to Integer

#### 题目

罗马数字包含以下七种字符：`I`， `V`， `X`， `L`，`C`，`D` 和 `M`。 

```javascript
字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

例如， 罗马数字 2 写做 `II` ，即为两个并列的 1。12 写做 `XII` ，即为 `X` + `II` 。 27 写做  `XXVII`, 即为 `XX` + `V` + `II` 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 `IIII`，而是 `IV`。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 `IX`。这个特殊的规则只适用于以下六种情况：

- `I` 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
- `X`可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。  
- `C` 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。

给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。 

示例：

```javascript
输入: "III"
输出: 3

输入: "IV"
输出: 4

输入: "IX"
输出: 9

输入: "LVIII"
输出: 58
解释: C = 100, L = 50, XXX = 30, III = 3.

输入: "MCMXCIV"
输出: 1994
解释: M = 1000, CM = 900, XC = 90, IV = 4.
```

标签： `数学` `字符串`

#### 解答

思路1：输入一个字符串，分析罗马字符，输出表达的数字，那就建立一个map表，循环这个字符串，将值相加；需要考虑3种特殊的情况，这3种情况触发都得去判断相邻的下一个字符，那就每次取相邻的两个字符去匹配map表的key，返回正确的数字；不适用for循环，将字符串转为数组，每次切掉开头已经判断过的字符；

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
  var map = {
    'I': 1,
    'V': 5,
    'X': 10,
    'L': 50,
    'C': 100,
    'D': 500,
    'M': 1000,
    'IV': 4,
    'IX': 9,
    'XL': 40,
    'XC': 90,
    'CD': 400,
    'CM': 900
  }
  var arr = s.split(''), result = 0;
  while(arr.length > 0){
    var cur = null;
    if (map[arr[0] + arr[1]] != null) {
      cur = map[arr[0] + arr[1]];
      arr.splice(0, 2);
    } else {
      cur = map[arr[0]];
      arr.splice(0, 1);
    }
    result += cur;
  }
  return result;
};
```

测试通过，但是时间很慢，感觉性能消耗在了`arr.aplice()`上面，查看一些其他解答，考虑使用for循环，命中特殊情况就将`i++`，所以思路1的思维方式还是有一些问题。

思路2：改for循环，弃用`arr.splice()`操作，试一试。

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
  var map = {
    'I': 1,
    'V': 5,
    'X': 10,
    'L': 50,
    'C': 100,
    'D': 500,
    'M': 1000,
    'IV': 4,
    'IX': 9,
    'XL': 40,
    'XC': 90,
    'CD': 400,
    'CM': 900
  }
  var arr = s.split(''), result = 0;
  for (let i = 0; i < arr.length; i++) {
    if (map[arr[i] + arr[i+1]] != null) {
      result += map[arr[i] + arr[i+1]];
      i++;
    } else {
      result += map[arr[i]];
    }
  }
  return result;
};
```

测试通过，速度有提升。方法2比方法1更简洁一些。这个题目绕在需要判断相邻的罗马数字，给出正确的对应数字。



























































