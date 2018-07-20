### 两个列表的最小索引总和 Minimum Index Sum of Two Lists 

#### 题目

假设Andy和Doris想在晚餐时选择一家餐厅，并且他们都有一个表示最喜爱餐厅的列表，每个餐厅的名字用字符串表示。

你需要帮助他们用**最少的索引和**找出他们**共同喜爱的餐厅**。 如果答案不止一个，则输出所有答案并且不考虑顺序。 你可以假设总是存在一个答案。

示例：

```javascript
输入:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
输出: ["Shogun"]
解释: 他们唯一共同喜爱的餐厅是“Shogun”。

输入:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
输出: ["Shogun"]
解释: 他们共同喜爱且具有最小索引和的餐厅是“Shogun”，它有最小的索引和1(0+1)。
```

**提示:**

1. 两个列表的长度范围都在 [1, 1000]内。
2. 两个列表中的字符串的长度将在[1，30]的范围内。
3. 下标从0开始，到列表的长度减1。
4. 两个列表都没有重复的元素。

标签： `哈希表`

#### 解答

思路1： 先将共有的字符串存入map表，同时找到最小的索引和。再去循环map表，将等于最小和的key拿出来，push到数组。

```javascript
/**
 * @param {string[]} list1
 * @param {string[]} list2
 * @return {string[]}
 */
var findRestaurant = function(list1, list2) {
  var map = Object.create(null), result = [], min = Infinity;
  for(var i = 0; i < list2.length; i++){
    var idx = list1.indexOf(list2[i]);
    if(idx > -1){
      map[list2[i]] = idx + i;
      min = Math.min(min, idx+i);
    }
  }
  for(key in map){
    if(map[key] === min){
      result.push(key);
    }
  }
  return result;
};
```

提交通过





