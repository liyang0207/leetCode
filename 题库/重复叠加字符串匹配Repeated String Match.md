### 重复叠加字符串匹配Repeated String Match

#### 题目

给定两个字符串 A 和 B, 寻找重复叠加字符串A的最小次数，使得字符串B成为叠加后的字符串A的子串，如果不存在则返回 -1。

举个例子，A = "abcd"，B = "cdabcdab"。

答案为 3， 因为 A 重复叠加三遍后为 “abcdabcdabcd”，此时 B 是其子串；A 重复叠加两遍后为"abcdabcd"，B 并不是其子串。

注意： `A` 与 `B` 字符串的长度在1和10000区间范围内。

#### 解答

思路1： 难点在于如何确定循环的次数，跟`A`和`B`的长度有关，想着叠加后的字符串最长应该是`A`和`B`大值的2倍。

```javascript
/**
 * @param {string} A
 * @param {string} B
 * @return {number}
 */
var repeatedStringMatch = function(A, B) {
  var blen = B.length, temp = A, flag = 1;
  var max = Math.max(temp.length, blen);
  while(A.length < max*3){
    if(A.indexOf(B) > -1) return flag;
    A += temp;
    flag++;
  }
  return -1;
};
```

提交通过。