### 种花问题 Can Place Flowers 

#### 题目

假设你有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花卉不能种植在相邻的地块上，它们会争夺水源，两者都会死去。

给定一个花坛（表示为一个数组包含0和1，其中0表示没种植花，1表示种植了花），和一个数 **n** 。能否在不打破种植规则的情况下种入 **n** 朵花？能则返回True，不能则返回False。

示例：

```javascript
输入: flowerbed = [1,0,0,0,1], n = 1
输出: True

输入: flowerbed = [1,0,0,0,1], n = 2
输出: False
```

**注意:**

1. 数组内已种好的花不会违反种植规则。
2. 输入的数组长度范围为 [1, 20000]。
3. **n** 是非负整数，且不会超过输入数组的大小。

标签： `数组`

#### 解答

思路1： 能不能种花，得看某一项在自己是0的情况下前后是不是也都是0，要注意一点是开头和结尾如果有两个0也是可以的`[0, 0, 1, ..., 1, 0, 0]`，那就先在数组的头尾都先加个0，然后循环数组，碰到符合条件的项，就将该项赋值为1，同时`i++`跳过下一项的循环。每次循环结束判断一下`n <= flag`是否成立，成立就提前结束循环，节省性能。

```javascript
/**
 * @param {number[]} flowerbed
 * @param {number} n
 * @return {boolean}
 */
var canPlaceFlowers = function(flowerbed, n) {
  flowerbed.push(0);
  flowerbed.unshift(0);
  var len = flowerbed.length, flag = 0;
  for(var i = 1; i < len-1; i++){
    if(flowerbed[i-1] + flowerbed[i] + flowerbed[i+1] === 0){
      flag++;
      flowerbed[i] = 1;
      i++;
    }
    if(n <= flag){ return true; }
  }
  return false;
};
```

提交通过，思路感觉还可以，简单易懂。