### 分发饼干Assign Cookies

#### 题目

假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。对每个孩子 i ，都有一个胃口值 gi ，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j ，都有一个尺寸 sj 。如果 sj >= gi ，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

**注意：**

你可以假设胃口值为正。
一个小朋友最多只能拥有一块饼干。

示例：

```javascript
输入: [1,2,3], [1,1]

输出: 1

解释: 
你有三个孩子和两块小饼干，3个孩子的胃口值分别是：1,2,3。
虽然你有两块小饼干，由于他们的尺寸都是1，你只能让胃口值是1的孩子满足。
所以你应该输出1。

输入: [1,2], [1,2,3]

输出: 2

解释: 
你有两个孩子和三块小饼干，2个孩子的胃口值分别是1,2。
你拥有的饼干数量和尺寸都足以让所有孩子满足。
所以你应该输出2
```

#### 解答

思路1：双层循环，内层循环找到大于等于胃口的最小值，结果加一，同时将该值从数组中删除，最后返回结果值。

```javascript
/**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
var findContentChildren = function(g, s) {
  var result = 0;
  for(var i = 0; i < g.length; i++){
    var cur = g[i], min = Infinity, slen = s.length;
    for(var j = 0; j < slen; j++){
      if(s[j] >= cur && s[j] < min){
        min = s[j];
      }
    }
    if(min !== Infinity){
      result++;
      s.splice(s.indexOf(min), 1);
    }
  }
  return result;
};
```

提交通过，但是性能很差。

思路2：分别排序两个数组，只有当尺寸值大于等于胃口值时，才将胃口值的flag位置往后移动一位，然后继续判断。

```javascript
/**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
var findContentChildren = function(g, s) {
  g.sort((a, b) => a - b);
  s.sort((a, b) => a - b);
  var res = 0;
  s.forEach((num) => {
    if(num >= g[res]) res++;
  })
  return res;
};
```

提交通过。

