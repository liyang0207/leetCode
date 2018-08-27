### 棒球比赛 Baseball Game

你现在是棒球比赛记录员。 给定一个字符串列表，每个字符串可以是以下四种类型之一： 1.`整数`（一轮的得分）：直接表示您在本轮中获得的积分数。 2. `"+"`（一轮的得分）：表示本轮获得的得分是前两轮`有效` 回合得分的总和。 3. `"D"`（一轮的得分）：表示本轮获得的得分是前一轮`有效` 回合得分的两倍。 4. `"C"`（一个操作，这不是一个回合的分数）：表示您获得的最后一个`有效` 回合的分数是无效的，应该被移除。 每一轮的操作都是永久性的，可能会对前一轮和后一轮产生影响。 你需要返回你在所有回合中得分的总和。

示例：

```javascript
输入: ["5","2","C","D","+"]
输出: 30
解释: 
第1轮：你可以得到5分。总和是：5。
第2轮：你可以得到2分。总和是：7。
操作1：第2轮的数据无效。总和是：5。
第3轮：你可以得到10分（第2轮的数据已被删除）。总数是：15。
第4轮：你可以得到5 + 10 = 15分。总数是：30。

输入: ["5","-2","4","C","D","9","+","+"]
输出: 27
解释: 
第1轮：你可以得到5分。总和是：5。
第2轮：你可以得到-2分。总数是：3。
第3轮：你可以得到4分。总和是：7。
操作1：第3轮的数据无效。总数是：3。
第4轮：你可以得到-4分（第三轮的数据已被删除）。总和是：-1。
第5轮：你可以得到9分。总数是：8。
第6轮：你可以得到-4 + 9 = 5分。总数是13。
第7轮：你可以得到9 + 5 = 14分。总数是27。
```

**注意：**

- 输入列表的大小将介于1和1000之间。
- 列表中的每个整数都将介于-30000和30000之间。

#### 解答

思路1：利用`switch`语句，针对不同的情况，利用数组模拟栈，最后计算总和。

```javascript
/**
 * @param {string[]} ops
 * @return {number}
 */
var calPoints = function(ops) {
  var arr = [];
  for(var i = 0; i < ops.length; i++){
    var len = arr.length;
    switch(ops[i]){
      case '+':
        arr.push(arr[len-1]+arr[len-2]);break;
      case 'D':
        arr.push(arr[len-1] * 2);break;
      case 'C':
        arr.pop();break;
      default:
        arr.push(+ops[i]);break;
    }
  }
  return arr.reduce((prev, next) => {
    return prev + next;
  }, 0)
};
```

提交通过，但是速度比较慢，最后一步的`reduce`求和应该可以省去。

思路2：每次循环直接求和，省去`reduce`计算。

```javascript
/**
 * @param {string[]} ops
 * @return {number}
 */
var calPoints = function(ops) {
  var arr = [], sum = 0, round = 0;
  for(var i = 0; i < ops.length; i++){
    var len = arr.length;
    switch(ops[i]){
      case '+':
        round = arr[len-1]+arr[len-2];
        sum += round;
        arr.push(round);break;
      case 'D':
        round = arr[len-1] * 2;
        sum += round;
        arr.push(round);break;
      case 'C':
        round = arr[len-1];
        sum -= round;
        arr.pop();break;
      default:
        round = +ops[i];
        sum += round;
        arr.push(round);break;
    }
  }
  return sum;
};
```

提交通过。