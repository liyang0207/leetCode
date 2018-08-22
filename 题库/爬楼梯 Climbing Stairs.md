### 爬楼梯 Climbing Stairs

假设你正在爬楼梯。需要 *n* 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**注意：**给定 *n* 是一个正整数。

示例：

```javascript
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶

输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```

#### 解答

思路1：爬到第`n`层的方法是爬到第`n-1`层和第`n-2`的方法的和。也就是`F(n) = F(n-1) + F(n-2)`，不断循环。

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function(n) {
  if(n === 0) return 1;
  var stepA = 0, stepB = 1, i = 1, result = 0;
  while(i <= n){
    result = stepA + stepB;
    stepA = stepB;
    stepB = result;
    i++;
  }
  return result;
};
```

提交通过，不过这道题的答案就是一个斐波那契数列：`1,1,2,3,5,8,13,21,....`，感觉很奇妙，很好的题。