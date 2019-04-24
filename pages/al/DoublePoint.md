# 双指针法含义

双指针法是指并非使用单指针（并非狭义的指C C++中的指针，二十泛指 索引、游标等可以迭代的对象），使用双指针同向或者相向扫描，从而达到目的的一种解决思路。
双指针法充分使用了`数组有序`这一特征，从而在某些情况下能够简化一些运算。
## 双指针法应用
### 求和
#### 求合为sum的两个数
1. 两数之和
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。
```java
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];
        if (nums == null) {
            return res;
        }
        Map<Integer, Integer> map = new HashMap<>(nums.length);
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[]{map.get(target - nums[i]), i};
            } else {
                map.put(nums[i], i);
            }
        }
        return res;
    }
```
### 删除元素

#### 移除固定元素
 27. 移除元素
就地移除，可以更改元素位置。
```java
    public int removeElement(int[] nums, int val) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int i = 0;
        int j = nums.length;
        while (i < j) {
            if (nums[i] == val) {
                nums[i] = nums[j];
                j--;
            } else {
                i++;
            }
        }
        return j;
```

#### 删除排序数组中的重复项
26. 删除排序数组中的重复项

```java
     public int removeDuplicates(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
        int i = 0, j = 1;
        while (j < nums.length) {
            if (nums[i] == nums[j]) {
                //相等时，快指针进1
                j++;
            } else {
                //不相等时，快指针的值付给慢指针，慢指针进1
                nums[i + 1] = nums[j];
                i++;
                j++;
            }
        }
        return i + 1;//函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
    }
```

### 排序
#### 按奇偶排序数组
905. 按奇偶排序数组
给定一个非负整数数组 A，返回一个由 A 的所有偶数元素组成的数组，后面跟 A 的所有奇数元素。

你可以返回满足此条件的任何数组作为答案。。
```java
    待更新
```

### 排序
#### 盛最多水的容器
11. 盛最多水的容器。
为了保证面积的最大化，需要考虑指针的距离尽可能大，及面积尽可能'长'；在这种情况下，想高度靠拢，因为面积是靠长和宽（两个数中的最小值）两个因素决定的，如果移动较长的指针，面积还是依赖于短的指针，这样长减少，宽可能不会发生变化，距离面积最大化没有获得增加；相反，要是使得短指针向长的方向移动，即使缩短了长度，但是宽度得到了提高，可以克服长度减小带来的面积减少。
```java
     public int maxArea(int[] height) {
           int maxArea = 0, l = 0, r = height.length-1;
           while (l < r) {
               maxArea = Math.max(maxArea,(r - l) * (Math.min(height[l], height[r])));
               //始终使得短指针向长指针移动
               if (height[l] <= height[r]) {
                   l++;
               } else {
                   r--;
               }
           }
           return maxArea;
       }
```