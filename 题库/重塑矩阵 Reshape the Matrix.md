### 重塑矩阵 Reshape the Matrix 

#### 题目

在MATLAB中，有一个非常有用的函数 `reshape`，它可以将一个矩阵重塑为另一个大小不同的新矩阵，但保留其原始数据。

给出一个由二维数组表示的矩阵，以及两个正整数`r`和`c`，分别表示想要的重构的矩阵的行数和列数。

重构后的矩阵需要将原始矩阵的所有元素以相同的**行遍历顺序**填充。

如果具有给定参数的`reshape`操作是可行且合理的，则输出新的重塑矩阵；否则，输出原始矩阵。

示例：

```javascript
输入: 
nums = 
[[1,2],
 [3,4]]
r = 1, c = 4
输出: 
[[1,2,3,4]]
解释:
行遍历nums的结果是 [1,2,3,4]。新的矩阵是 1 * 4 矩阵, 用之前的元素值一行一行填充新矩阵。

输入: 
nums = 
[[1,2],
 [3,4]]
r = 2, c = 4
输出: 
[[1,2],
 [3,4]]
解释:
没有办法将 2 * 2 矩阵转化为 2 * 4 矩阵。 所以输出原矩阵。
```

**注意：**

1. 给定矩阵的宽和高范围在 [1, 100]。
2. 给定的 r 和 c 都是正数。

#### 解答

思路1： 双循环数组，外层循环行，内层循环列，不过要先将数组“抹平”，这样才能准确填充。

```javascript
/**
 * @param {number[][]} nums
 * @param {number} r
 * @param {number} c
 * @return {number[][]}
 */
var matrixReshape = function(nums, r, c) {
  if(nums.length * nums[0].length !== r*c){
    return nums;
  }
  var temp = [];
  for(var k = 0; k < nums.length; k++){
    temp = temp.concat(nums[k]);
  }
  console.log(temp);
  var result = [];
  for(var i = 0; i < r; i++){
    result[i] = [];
    for(var j = i*c; j < (i+1)*c; j++){
      result[i].push(temp[j]);
    }
  }
  return result;
};
```

提交通过。查看优秀答案，简化过程。

思路2：`concat`方法可以换成`...`操作符；注意`splice()`方法返回的是剪切掉的`数组`，正好可以拿来用，省去`result[i] = []`的过程。

```javascript
/**
 * @param {number[][]} nums
 * @param {number} r
 * @param {number} c
 * @return {number[][]}
 */
var matrixReshape = function(nums, r, c) {
  if (nums.length * nums[0].length !== r * c) return nums
  let res = []
  let arr = []
  for (let i = 0; i < nums.length; i++) {
    arr.push(...nums[i]);
  }
  for (let j = 0; j < r; j++) {
    res.push(nums.splice(0, c));
  }
  return res
};
```

这是比较清晰简化的过程，充分利用操作方法，简单明了，方便他人阅读。









