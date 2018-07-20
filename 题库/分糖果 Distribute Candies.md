### 分糖果 Distribute Candies 

#### 题目

给定一个**偶数**长度的数组，其中不同的数字代表着不同种类的糖果，每一个数字代表一个糖果。你需要把这些糖果**平均**分给一个弟弟和一个妹妹。返回妹妹可以获得的最大糖果的种类数。 

示例：

```javascript
输入: candies = [1,1,2,2,3,3]
输出: 3
解析: 一共有三种种类的糖果，每一种都有两个。
     最优分配方案：妹妹获得[1,2,3],弟弟也获得[1,2,3]。这样使妹妹获得糖果的种类数最多。
     
输入: candies = [1,1,2,3]
输出: 2
解析: 妹妹获得糖果[2,3],弟弟获得糖果[1,1]，妹妹有两种不同的糖果，弟弟只有一种。这样使得妹妹可以获得的糖果种类数最多。
```

**注意:**

1. 数组的长度为[2, 10,000]，并且确定为偶数。
2. 数组中数字的大小在范围[-100,000, 100,000]内。

标签： `哈希表`

#### 解答

思路1： 先建立糖果数量的map表，思路是先给哥哥补全糖果数量`len/2`，先将每种糖果多于1个的都分给哥哥，如果不够`len/2`，就给他补全，剩下的都是妹妹最多能拿到的糖果种类数。

```javascript
/**
 * @param {number[]} candies
 * @return {number}
 */
var distributeCandies = function(candies) {
  var map = {}, len = candies.length;
  for(var i = 0; i < len; i++){
    map[candies[i]] != null ? map[candies[i]]++ : map[candies[i]] = 1;
  }
  var arr = Object.keys(map), temp = 0;;
  for(var j = 0; j < arr.length; j++){
    temp = temp + map[arr[j]] - 1;
  }
  return temp < len/2 ? (arr.length + temp)/2 : arr.length; 
};
```

提交通过，查看优秀解答，发现一个更简单的逻辑解法。

思路2： 使用正则来解该题，简单优雅。

```javascript
/**
 * @param {number[]} candies
 * @return {number}
 */
var distributeCandies = function(candies) {
    return Math.min(new Set(candies).size, candies.length/2);
};
```

妹妹能分到的最多糖果数是糖果的种类数，或者糖果数的一半。有点绕不过来，会不会出现少于糖果种类的情况呢？





