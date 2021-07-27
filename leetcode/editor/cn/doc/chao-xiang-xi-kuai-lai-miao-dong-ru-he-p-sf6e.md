### 题目描述

判断给定数组里是否有重复元素。

### 思路解析

#### 方法一 排序

数组排序后，判断相邻元素是否相等。

```Java []
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 1; ++i) {
            if (nums[i] == nums[i + 1]) {
                return true;
            }
        }
        return false;
    }
}
```

时间复杂度 : ![O(n\logn) ](./p__O_n_log_n__.png) 。即排序的时间复杂度。扫描的时间复杂度 *O(n)* 可忽略。

空间复杂度 : *O(1)*。 没有用到额外空间。如果深究 `Arrays.sort(nums)` 使用了栈空间，那就是 ![O(\logn) ](./p__O_log_n__.png) 。

---

#### 方法二 使用 set

遍历数组，数字放到 `set` 中。如果数字已经存在于 `set` 中，直接返回 `true`。如果成功遍历完数组，则表示没有重复元素，返回 `false`。

```Java []
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num: nums) {
            if (set.contains(num)) {
                return true;
            }
            set.add(num);
        }
        return false;
    }
}
```

#### 方法二之炫技

这题可以一行代码解决。
Java 可以用 stream 实现一行将 `int[]` 转成 `Set<Integer>` 。为了更简短一些，可以直接利用 stream 的 `distinct` 和 `count` 算子。
如果使用 Python 那更简单： `len(set(nums)) != len(nums)`。

代码如下：

``` java [set-Java]
class Solution {
    public boolean containsDuplicate(int[] nums) {
        return IntStream.of(nums).distinct().count() != nums.length;
    }
}
```

``` python [set-Python]
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        return len(set(nums)) != len(nums)
```


时间复杂度 : *O(n)*

空间复杂度 : *O(n)*


### 题目拓展

这题类似题型非常之多，而且 **大多都是面试高频题** 。

* [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)
题目额外限定了数组元素的大小范围，所以有时间复杂度 *O(n)*，空间复杂度 *O(1)* 的做法。

* [287. 寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number/)
题目也是额外限定了数组元素的大小范围（注意限定条件和上题不同！），最优做法是快慢指针。关于快慢指针的练习，还可以看这题快乐一下：[202. 快乐数](https://leetcode-cn.com/problems/happy-number/)，我精心写了题解。

* [26. 删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)
做法也是快慢指针。非常经典的题目，C++ 标准库的 `unique` 方法就是 [这么实现的](http://www.cplusplus.com/reference/algorithm/unique/)。非常值得一刷。

* [136. 只出现一次的数字](https://leetcode-cn.com/problems/single-number/)
超级经典，我相信绝大多数人已经做过了，没有做过的速速去会会它。姊妹题：[137. 只出现一次的数字 II](https://leetcode-cn.com/problems/single-number-ii/) 和 [260. 只出现一次的数字 III](https://leetcode-cn.com/problems/single-number-iii/)。这两题也是必刷题，刷了以后会对异或有更深入的了解和认识。其中 [剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/) 是重复题目，我提供了一种 [使用二分解决的思路](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/solution/shi-yao-zhe-ti-huan-ke-yi-yong-er-fen-cha-zhao-bi-/)，值得一看哦～

