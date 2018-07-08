### 杨辉三角 Pascals Triangle

#### 题目

给定一个非负整数 *numRows，*生成杨辉三角的前 *numRows* 行。 在杨辉三角中，每个数是它左上方和右上方的数的和。 

示例：

```javascript
输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

标签： `数组`

#### 解答

思路1：最初想的是寻找杨辉三角每一行中每一项的规律，发现单纯使用数学规律没有办法计算出每一项的值；既然每一项是左上角和右上角的和，那就两次循环，取上一行对应的两个值，相加；

```javascript
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
  var result = [];
  for(var i = 1; i <= numRows; i++) {
    if (i === 1) { result = [[1]];continue; }
    var item = [0].concat(result[i - 2], 0);
    var temp = [];
    for (var j = 1; j <= i; j++) {
      temp.push(item[j-1] + item[j]);
    }
    result.push(temp);
  }
  return result;
};
```

提交测试通过，查看一些比较优秀的解答，发现其实可以省去中间的`temp`变量，但因为结果是一个二维数组，需要提前将结果的第`i`项设为空数组。

思路2：整理不必要的变量。

```javascript
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
  var result = [];
  for(var i = 0; i < numRows; i++) {
    result.push(new Array(i+1));
    result[i][0] = 1;
    result[i][result[i].length - 1] = 1;
    for(var j = 1; j < i; j++){
      result[i][j] = result[i-1][j-1] + result[i-1][j];  
    }
  }
  return result;
};
```

