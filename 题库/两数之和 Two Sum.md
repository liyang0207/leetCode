### 两数之和 Tow Sum

#### 题目

给定一个整数数组和一个目标值，找出数组中和为目标值的**两个**数。你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

示例：

```javascript
给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

标签： `数组` `哈希表`

#### 解答

思路1：第一次思考，题目限定每个输入只有一种答案，数组元素为整数（脑袋里要考虑负数和0的情况），那就直接循环两次进行加的运算，找到值。

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    for (var i = 0; i < nums.length - 1; i++) {
        for(var j = i+1; j< nums.length; j++) {
            if (nums[i] + nums[j] === target) {
                return [i, j];
            }
        }
    }
};
```

提交通过，测试用时144ms，	大概排提交答案速度的前74.56%，最好的用52ms，有比较集中的在72ms左右。查看阅读解答及比较优秀的答案，总结下面的思路2。

复杂度：

- 时间复杂度：`O(n2)`，对于每个元素，我们试图通过遍历数组的其余部分来寻找它所对应的目标元素，这将耗费 `O(n)`的时间。
- 空间复杂度：`O(1)`。

思路2：可以使用哈希表来循环一次实现（哈希表概念目前不是很清晰），循环的时候建立数组值=>索引的对应关系，因为最后要return的是结果索引组成的数组，我们判断Map表（哈希表？）中是否存在`target-x`的key，找到了就直接返回这个key的value，即索引。引用官方说法：

> 在进行迭代并将元素插入到表中的同时，我们还会回过头来检查表中是否已经存在当前元素所对应的目标元素。如果它存在，那我们已经找到了对应解，并立即将其返回。 

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    var Map = {};
    for (var i = 0; i < nums.length; i++) {
        var x = nums[i];
        var y = Map[target - x];
        if (y != null) {
            return [y, i];
        }
        Map[x] = i;
    }
};
```

提交通过，测试用时84ms，排名87.29%，速度有比较大的提升。

复杂度：

- 时间复杂度：`O(n)`，遍历了包含有`n`个元素的列表一次。在表中进行的每次查找只花费 `O(1)`的时间。 
- 空间复杂度：`O(n)`，所需的额外空间取决于哈希表中存储的元素数量，该表最多需要存储`n`个元素。 