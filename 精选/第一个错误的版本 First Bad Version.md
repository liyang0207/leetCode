### 第一个错误的版本 First Bad Version

#### 题目

你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 `n` 个版本 `[1, 2, ..., n]`，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 `bool isBadVersion(version)` 接口来判断版本号 `version` 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

示例：

```javascript
给定 n = 5，并且 version = 4 是第一个错误的版本。

调用 isBadVersion(3) -> false
调用 isBadVersion(5) -> true
调用 isBadVersion(4) -> true

所以，4 是第一个错误的版本。 
```

#### 解答

思路1：最早想的是将整数转为`[1, 2, 3, ..., n]`的数组，然后不断判断中值是否为`badVersion`，最后数组剩余一个元素，就是目标值，但是发现当`n`特别大时，生成数组的循环次数太多，超过限制。后来想其实可以直接判断值，不是必须要转为数组。

```javascript
/**
 * Definition for isBadVersion()
 * 
 * @param {integer} version number
 * @return {boolean} whether the version is bad
 * isBadVersion = function(version) {
 *     ...
 * };
 */

/**
 * @param {function} isBadVersion()
 * @return {function}
 */
var solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    return function(n) {
      var start = 1, end = n;
      while(start !== end){
        var mid = Math.floor((start + end)/2);
        isBadVersion(mid) ? end = mid : start = ++mid;
      }
      return start
    };
};
```

提交通过，但是运行时间不是特别好。大概80+ms，但是50ms左右的答案其实思路一样，但是多了一步判断，当中值是`badVersion`时，判断一下上一个值是不是`badVersion`，如果不是，那么这个中值就是目标值，不需要再继续二分下去，省去很多循环。

思路2：中值是`badVersion`时，判断一次`中值-1`是不是`badVersion`，可能省去很多次循环。

```javascript
/**
 * Definition for isBadVersion()
 * 
 * @param {integer} version number
 * @return {boolean} whether the version is bad
 * isBadVersion = function(version) {
 *     ...
 * };
 */

/**
 * @param {function} isBadVersion()
 * @return {function}
 */
var solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    return function(n) {
      var start = 1, end = n;
      while(start <= end){
        var mid = Math.floor((start + end)/2);
        if(isBadVersion(mid)){
          if(!isBadVersion(mid-1)) return mid; 
          end = mid
        } else {
          start = ++mid
        }
      }
    };
};
```

提交通过。