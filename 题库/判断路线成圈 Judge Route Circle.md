### 判断路线成圈 Judge Route Circle

#### 题目

初始位置 (0, 0) 处有一个机器人。给出它的一系列动作，判断这个机器人的移动路线是否形成一个圆圈，换言之就是判断它是否会移回到**原来的位置**。

移动顺序由一个字符串表示。每一个动作都是由一个字符来表示的。机器人有效的动作有 `R`（右），`L`（左），`U`（上）和 `D`（下）。输出应为 true 或 false，表示机器人移动路线是否成圈。

示例：

```javascript
输入: "UD"
输出: true

输入: "LL"
输出: false
```

#### 解答

思路1：建立map表，循环字符串内给字符的数量，最后判断`L`和`R`，`U`和`B`的数量是否一致。

```javascript
/**
 * @param {string} moves
 * @return {boolean}
 */
var judgeCircle = function(moves) {
  var map = {};
  for(var i = 0; i < moves.length; i++){
    var cur = moves[i];
    map[cur] ? map[cur]++ : map[cur] = 1;
  }
  return map['L'] === map['R'] && map['U'] === map['D'];
};
```

提交通过。