### 删除排序数组中的重复项 Remove Duplicates from Sorted Array

### 题目

给定一个排序数组，你需要在**原地**删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在**原地修改输入数组**并在使用 O(1) 额外空间的条件下完成。

示例：

```javascript
给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。

给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。
```

标签：`数组` `双指针`

#### 解答

思路1：直接for循环数组，碰到与之前重复的项就直接`splice(i, 1)`截取掉，暴力操作数组，不过目测性能应该很差。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
  for (let i = 1; i < nums.length; i++ ) {
    if (nums[i-1] === nums[i]) {
      nums.splice(i, 1);
      i--;
    }
  }
  return nums.length;
};
```

测试通过，但是性能很差，运行时间很久。查看解答，使用双指针法，一个快指针，一个慢指针，将非重复的后面项复制到慢指针后面的位置，这样最后慢指针的位置就是数组的长度（+1）。

思路2：使用双指针法，不断复制后面非重复的值到前面去，慢指针走过的路就是所有符合题目要求的数组项。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
  let j = 0;   // 慢指针
  for (let i = 1; i < nums.length; i++) {
    if (nums[j] != nums[i]) {
      j++;
      nums[j] = nums[i];
    }
  }
  return ++j;
};
```

测试通过，用时比较短，这里只需要循环和复制值，省去了操作数组的过程，提示了不少性能。双指针法是个比较不错的方法，之后应该还会遇到类似的使用场景，需要好好理解。