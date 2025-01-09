
**287. 寻找重复数**
方法：二分查找
```python
def findDuplicate(self, nums: List[int]) -> int:
    min_val = 1  # 最小值
    max_val = len(nums)  # 最大值
    while min_val < max_val:
        mid = (min_val + max_val) // 2
        # 计算有多少个数在[1,mid]内
        cnt = sum(min_val <= num <= mid for num in nums)
        if cnt > (mid - min_val + 1):  # 重复数在[min_val, mid]内
            max_val = mid
        else:  # 重复数在[mid + 1, max_val]内
            min_val = mid + 1
    return min_val
```

**167. 两数之和 II - 输入有序数组**
方法：双指针
```python
def twoSum(self, numbers: List[int], target: int) -> List[int]:
    left = 0
    right = len(numbers) - 1
    while left < right:
        s = numbers[left] + numbers[right]
        if s == target:
            break
        if s > target:
            right -= 1
        else:
            left += 1
    return [left + 1, right + 1]
```


