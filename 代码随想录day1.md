## 704. Binary Search
[文档链接](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html#%E6%80%9D%E8%B7%AF)
[视频链接](https://www.bilibili.com/video/BV1fA4y1o715)
状态：最优解决。

暴力求解：直接遍历数组，逐个检查数组的每个元素是否和目标值相等。
时间复杂度：O(n)，最坏的情况是遍历全部数组。
空间复杂度：O(1)，只是用了一个循环变量，没有使用额外的数据结构。

方法：二分法。
使用条件：**数组有序**，无重复元素。
每次查找将数组长度减半。
注意 **左闭右开** 与 **左闭右闭** 的区别。我更习惯使用左闭右闭的方式。

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] < target:
                left = mid + 1
            elif nums[mid] > target:
                right = mid - 1
            else:
                return mid
        return -1
```

时间复杂度：O(log n)。
空间复杂度：O(1)。

LeetCode 35, 34, 69, 367 作为额外题目也都解决了。思路与方法大同小异。

## 27. Remove Element
[文档链接](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
[视频链接](https://www.bilibili.com/video/BV12A4y1Z7LP)
状态：最优解决。

暴力求解：两个for循环，一个for循环用于检测需要删除的元素；另一个for循环用于检测到需要删除的元素时，把删除元素后的所有元素往前移动一位。
时间复杂度：O(n^2)，最坏的情况第一个for循环下每次都执行第二个for循环，非常麻烦。
空间复杂度：O(1)，只是用了两个循环变量，没有使用额外的数据结构。

方法：双指针。使用一个for循环完成两个for循环的任务。要明确双指针分别指的是什么东西。
快指针：数组中的元素；慢指针：数组中非删除项的元素。

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left = 0
        for right in range(len(nums)):
            if nums[right] != val:
                nums[left] = nums[right]
                left += 1
        return left
```
时间复杂度：O(n)，只有一个循环。
空间复杂度：O(1)。
LeetCode 26, 283 作为额外题目也都解决了。

## 844. Backspace String Compare 

尽管本题也可以用双指针解决，但是我更习惯用list的内置函数解决。当检测到 # 的时候并且结果串不为空的时候，直接pop即可。

```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        def strOutput(s: str) -> str:
            result = []
            for char in s:
                if char != '#':
                    result.append(char)
                elif result:  # 如果有字符可以删除
                    result.pop()
            return ''.join(result)
        
        return strOutput(s) == strOutput(t)
```

## 977. Squares of a Sorted Array

同样是双指针的方法，只是这次的指针一个从头开始，一个从末尾开始，循环结束后将list翻转即可。

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        left = 0
        right = len(nums) - 1
        result = []
        while right >= left:
            if abs(nums[right]) >= abs(nums[left]):
                result.append(nums[right] * nums[right])
                right -= 1
            else:
                result.append(nums[left] * nums[left])
                left += 1
        return result[::-1]
```

时间复杂度：O(n)。只用一次循环即可。
空间复杂度：O(n)。需要一个新的数组来储存平方后的数组，除此之外只使用了常数级别的额外空间，例如循环变量。

今日收获：
数组部分是以前就刷过的题目。今天再刷，基本还都是掌握的。只有一些list和string的内置函数的用法需要再注意。