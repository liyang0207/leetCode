### 杨辉三角II Pascals TriangleII

#### 题目

给定一个非负索引 *k*，其中 *k* ≤ 33，返回杨辉三角的第 *k* （索引）行。 注意*k*从0开始。 在杨辉三角中，每个数是它左上方和右上方的数的和。 

示例：

```javascript
输入: 5
输出:
[1,4,6,4,1]
```

标签： `数组`

#### 解答

思路1：这道题比生成`杨辉三角`的那道题更进了一步，要求直接返回指定行，如果一行一行生成杨辉三角，然后返回最后一行，这题目就没有什么意思了。不过要吐槽的一点是`leetCode`中文网的翻译，说是返回第`k`行，结果却是要返回第`k+1`行（k从0开始）。这道题直接用公式，杨辉三角第n行的第m项为C(n-1, m-1)，即为从n-1个不同元素中取m-1个元素的组合数 ；

```javascript
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
  var result = [];
  for(var i = 0; i <= rowIndex; i++){
    var t = 1, b = 1;
    for(var j = 0; j < i; j++){
      t = (rowIndex - j) * t;
      b = (i - j) * b;
    }
    result.push(t/b);
  }
  return result;
};
```

提交测试通过。这道题中文网只有`1.8k/3.5k`的`通过/提交`，估计很多都是吐槽翻译才不想提交答案的吧。