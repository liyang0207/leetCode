### 盛最多水的容器 Container With Most Water

#### 题目

给定 *n* 个非负整数 *a*1，*a*2，...，*a*n，每个数代表坐标中的一个点 (*i*, *ai*) 。在坐标内画 *n* 条垂直线，垂直线 *i* 的两个端点分别为 (*i*, *ai*) 和 (*i*, 0)。找出其中的两条线，使得它们与 *x* 轴共同构成的容器可以容纳最多的水。

**说明：**你不能倾斜容器，且 *n* 的值至少为 2。

示例：

```javascript
输入: [1,8,6,2,5,4,8,3,7]
输出: 49
```

#### 解答

思路1：粗暴循环，对于每一个元素都去计算它跟它之前的元素的面积，找到最大的面积。

```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
  var maxArea = 0;
  for(var i = 1; i < height.length; i++){
    for(var j = 0; j < i; j++){
      var curArea = Math.min(height[i], height[j]) * (i - j);
      maxArea = Math.max(curArea, maxArea);
    }
  }
  return maxArea;
};
```

提交通过，但是过于粗暴，性能很差。

思路2：最大的面积最有可能出现在两侧的项组成，分别从左侧和右侧像中间去找最大面积，不断向中间逼近。

```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
  var maxArea = 0, left = 0, right = height.length - 1;
  while(left < right){
    maxArea = Math.max(Math.min(height[left], height[right]) * (right - left), maxArea);
    height[left] < height[right] ? left++ : right--;
  }
  return maxArea;
};
```

这个解法要好很多，计算次数`n`，速度要快很多。中等难度的题目就要开始抽象思考问题了，不能再以简单的方式去粗暴解决，有些问题不能具体去想，要逐渐开始抽象。

