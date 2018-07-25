### 自除数 Self Dividing Numbers 

#### 题目

*自除数* 是指可以被它包含的每一位数除尽的数。

例如，128 是一个自除数，因为 `128 % 1 == 0`，`128 % 2 == 0`，`128 % 8 == 0`。

还有，自除数不允许包含 0 。

给定上边界和下边界数字，输出一个列表，列表的元素是边界（含边界）内所有的自除数。

示例：

```javascript
输入： 
上边界left = 1, 下边界right = 22
输出： [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]
```

**注意：**

- 每个输入参数的边界满足 `1 <= left <= right <= 10000`。

标签： `数学`

#### 解答

思路1： 循环范围`left`到`right`，每一个数都要判断它的每一位跟它的余数，数字只能先转成字符串来取每一位，然后就想到借用`Array.prototype.every.call()`，每一项都满足才返回`true`。

```javascript
/**
 * @param {number} left
 * @param {number} right
 * @return {number[]}
 */
var selfDividingNumbers = function(left, right) {
  var remainder = 0, result = [], flag = true;
  for(var n = left; n <= right; n++){
    flag = Array.prototype.every.call(n.toString(), (s) => {
      return n % s === 0;
    })
    if(flag) result.push(n);
  }
  return result;
};
```

提交通过，自我感觉写的方法很不错，简单明了。
