### 买卖股票的最佳时机 Best Time to Buy and Sell Stock

#### 题目

给定一个数组，它的第 *i* 个元素是一支给定股票第 *i* 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。

示例：

```javascript
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
     
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

标签： `数组` `动态规划`

#### 解答

思路1：双for循环，将每一项作为初始值，计算其与其之后项的差值，存入结果数组，取出最大值。

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
  var len = prices.length;
  var result = [];
  for(var i = 0; i < len - 1; i++){
    var gap;
    for(var j = i+1; j < len; j++){
      gap = prices[j] - prices[i];
      if (result[i]) {
        result[i] = result[i] > gap ? result[i] : gap;
      } else {
        result[i] = gap;
      }
    }
  }
  result.sort((a, b) => { return b - a; });
  return (result[0] > 0) ? result[0] : 0;
};
```

提交测试通过，但性能极差，耗时很久。查看优秀解答优化思路，发现只需要单次循环，取一个`min`变量存放最小的值，每次循环往后走的时候，取当前项和`min`中的小值作为新的`min`，然后每次都会计算当前项和目前最小值之间的差值，再存入最大值内，一直循环到最后即可。

思路2：定义一个`min`值存放每次循环最小的值，`p`来存放最大收益值，循环一遍即可。

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
  let min = prices[0];
  let p = 0;
  let len = prices.length;
  for(let i = 0; i < len; i++){
    p = prices[i] - min > p ? prices[i] - min : p;
    if(prices[i] < min){
      min = prices[i]
    }
  }
  return p;
};
```

一次循环即可，不需要两次循环，然后再存值，再判断。