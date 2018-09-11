### 下一个排列 Next Permutation

#### 题目

实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须**原地**修改，只允许使用额外常数空间。

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
`1,2,3` → `1,3,2`
`3,2,1` → `1,2,3`
`1,1,5` → `1,5,1`

#### 解答

思路1：从后往前循环，找到第一个拐点，即数字先增加，后减少的地方，记录开始位置为`flag`；需要循环这一段数组，先再次从后往前循环，找到第一个比`flag`大的数，交换两者位置（之后的数都会比第一个找到的数大），最后对`flag+1`之后的数组做一个从小到大的排序即可。

```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var swap = function(arr, a, b){
  var temp = arr[a];
  arr[a] = arr[b];
  arr[b] = temp;
}
var sortFromIndex = function(arr, start){
  for(var k = start; k < arr.length - 1; k++){
    for(var q = k + 1; q < arr.length; q++){
      if(arr[k] > arr[q]){
        swap(arr, k, q)
      }
    }
  }
}
var nextPermutation = function(nums) {
  for(var i = nums.length - 2; i >=0; i--){
    if(nums[i] < nums[i+1]){
      for(var j = nums.length-1; j >= 0; j--){
        if(nums[i] < nums[j]){
          swap(nums, i, j);
          sortFromIndex(nums, i+1);
          return;
        }
      }
    }
  }
  nums.sort((a, b) => a - b);
};
```

自己的思路是没有问题的，但是实现方法一直不理想。这里将两个常用的方法抽出来，方便后面的逻辑调用。