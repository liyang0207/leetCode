### 亲密字符串Buddy Strings

#### 题目

给定两个由小写字母构成的字符串 `A` 和 `B` ，只要我们可以通过交换 `A` 中的两个字母得到与 `B` 相等的结果，就返回 `true` ；否则返回 `false` 。

示例：

```javascript
输入： A = "ab", B = "ba"
输出： true

输入： A = "ab", B = "ab"
输出： false

输入： A = "aa", B = "aa"
输出： true

输入： A = "aaaaaaabc", B = "aaaaaaacb"
输出： true

输入： A = "", B = "aa"
输出： false
```

提示：

1. `0 <= A.length <= 20000`
2. `0 <= B.length <= 20000`
3. `A` 和 `B` 仅由小写字母构成。

#### 解答

思路1：最早思路有些混乱，想着先循环字符串找到`A`和`B`不一样的两个字符的位置，然后交换两个字符的位置再跟`B`进行对比，但是这样对于`aa`-`aa`和`ab`-`ab`两种情况都无法判断。看了下阅读解答，分成两种情况：1. `A[i] === A[j] === B[i] === B[j]`也就是`A === B`的情况，这个时候需要看`A`里面是否有两个一样的字符；2. `A[i] === B[j], A[j] === B[i]`这种情况就是正常逻辑下的判断思路。

```javascript
/**
 * @param {string} A
 * @param {string} B
 * @return {boolean}
 */
var buddyStrings = function(A, B) {
  var flag1 = null, flag2 = null;
  if(A.length !== B.length) return false;
  if(A === B){
    for(var i = 0; i < A.length; i++){
      if(A.indexOf(A[i], i+1) > -1) return true;
    }
  } else {
    for(var i = 0; i < A.length; i++){
      if(A[i] !== B[i]){
        flag1 == null ? flag1 = i : flag2 = i;
      }
      if(flag2) break;
    }
    if(A[flag1] === B[flag2] && A[flag2] === B[flag1]) return true
  }
  return false;
};
```

这道题关键是想明白如何处理`aa`-`aa`和`ab`-`ab`这种情况。