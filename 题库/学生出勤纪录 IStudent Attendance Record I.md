### 学生出勤纪录 IStudent Attendance Record I

 #### 题目

给定一个字符串来代表一个学生的出勤纪录，这个纪录仅包含以下三个字符：

1. **'A'** : Absent，缺勤
2. **'L'** : Late，迟到
3. **'P'** : Present，到场

如果一个学生的出勤纪录中不**超过一个'A'(缺勤)**并且**不超过两个连续的'L'(迟到)**,那么这个学生会被奖赏。

你需要根据这个学生的出勤纪录判断他是否会被奖赏。

示例：

```javascript
输入: "PPALLP"
输出: True

输入: "PPALLL"
输出: False
```

#### 解答

思路1：这是一个找字符串中某个字符数量的问题，其中`A`不能超过一个，`LLL`不能出现，否则返回`false`。直接循环字符串，记录`A`出现的次数，超过1次直接返回`false`；同时记录`LLL`出现的次数，方法是遇见`L`就将flag加一，一旦不是`L`就将flag置0，一直到flag为3的时候，返回`false`。

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var checkRecord = function(s) {
  var num1 = 0, num2 = 0;
  for(var i = 0; i < s.length; i++){
    if(s[i] === 'L'){
      num2++;
      if(num2 === 3) return false;
      continue;
    }else{
      num2 = 0;
    }
    if(s[i] === 'A'){
      num1++;
      if(num1 > 1) return false;
    }
  }
  return true;
};
```

提交通过。

思路2：直接使用正则`match`来解决，看返回的数组长度来判断。不过这种方法需要两次正则，而且貌似必须找完整个字符串才行，可能性能有点差，不过也不一定。

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var checkRecord = function(s) {
  var astore = s.match(/A/g);
  if(astore && astore.length > 1) return false;
  var lstore = s.match(/LLL/g);
  if(lstore) return false;
  return true;
};
```

方法看起来能简洁一点吧。











