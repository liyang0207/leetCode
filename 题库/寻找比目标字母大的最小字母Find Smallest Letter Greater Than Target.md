### 寻找比目标字母大的最小字母Find Smallest Letter Greater Than Target

#### 题目

给定一个只包含小写字母的有序数组`letters` 和一个目标字母 `target`，寻找有序数组里面比目标字母大的最小字母。

数组里字母的顺序是循环的。举个例子，如果目标字母`target = 'z'` 并且有序数组为 `letters = ['a', 'b']`，则答案返回 `'a'`。

示例：

```javascript
输入:
letters = ["c", "f", "j"]
target = "a"
输出: "c"

输入:
letters = ["c", "f", "j"]
target = "c"
输出: "f"

输入:
letters = ["c", "f", "j"]
target = "d"
输出: "f"

输入:
letters = ["c", "f", "j"]
target = "g"
输出: "j"

输入:
letters = ["c", "f", "j"]
target = "j"
输出: "c"

输入:
letters = ["c", "f", "j"]
target = "k"
输出: "c"
```

**注:**

1. `letters`长度范围在`[2, 10000]`区间内。
2. `letters` 仅由小写字母组成，最少包含两个不同的字母。
3. 目标字母`target` 是一个小写字母。

#### 解答

思路1：二分法，逐步判断

```javascript
/**
 * @param {character[]} letters
 * @param {character} target
 * @return {character}
 */
var nextGreatestLetter = function(letters, target) {
  if(target >= letters[letters.length - 1]) return letters[0];
  while(letters.length > 1){
    var midIdx = Math.floor(letters.length / 2);
    if(target < letters[midIdx]){
      if(target >= letters[midIdx-1]) return letters[midIdx];
      letters.splice(midIdx);
    }else{
      letters.splice(0, midIdx+1)
    }
  }
  return letters[0]
};
```

提交通过，不过有意思的是这道题直接循环寻找目标值速度要快的多。

