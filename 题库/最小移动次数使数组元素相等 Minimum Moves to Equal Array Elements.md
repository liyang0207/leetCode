### 最小移动次数使数组元素相等 Minimum Moves to Equal Array Elements 

### 题目

给定一个长度为 *n* 的**非空**整数数组，找到让数组所有元素相等的最小移动次数。每次移动可以使 *n* - 1 个元素增加 1。 

示例：

```javascript
输入:
[1,2,3]

输出:
3

解释:
只需要3次移动（注意每次移动会增加两个元素的值）：

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

标签： `数学`

#### 解答

思路1： 将数组排序，每次除最后一项外，其余各项都增加`count`（最大值减最小值）大小，然后比较最后一项和他前一项，如果相等，则说明各项都已经一样；否则，将`flag`移至`len-2`处，此时最大项是`len-2`，最小项是`len-1`，除最大项外其他各项都增加`count`（最大值减最小值，即`len-2`减去`len-1`），一直循环，直到这一项等于前一项。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var minMoves = function(nums) {
  var len = nums.length, count = 0, temp = 0, flag = len -1;
  if(len === 1) return 0;
  nums.sort((a, b) => { return a - b; });
  while(true){
    if(flag === len-1){
      temp = nums[flag] - nums[0]
    }else{
      temp = nums[flag] - nums[flag+1]
    }
    count = count + temp;
    for(var i = 0; i < len; i++){
      if(i !== flag){
        nums[i] = nums[i] + temp;
      }
    }
    if(nums[flag] === nums[flag-1]) break;
    flag--;
  }
  return count; 
};
```

提交通过。但是速度非常慢，感觉差点都通过不了。查看优秀解法，发现`count`值就为数组各项与最小值的差值和。

思路2：

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var minMoves = function(nums) {
  let min=nums[0], sum=0;
  nums.forEach(function (num) {
    min = Math.min(num,min);
  });
  nums.forEach(function (num) {
    sum+=num-min;
  });
  return sum;
};
```

这个解法比较快，但不是很懂。不过发现一个有意思的地方，这里他判断数组的最小项是通过`forEach`不断的比对，而我一般习惯使用数组自带的`sort()`方法排序，然后取第一项。那这两种方法哪种更快呢？简单在浏览器里打印了一下，发现速度差距很小，但是`forEach`方法要更快一些。

















