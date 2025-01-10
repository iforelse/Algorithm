
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

**300. 最长递增子序列**
方法：子集型回溯（动态规划）（视频还有更优的 贪心+二分查找）
```python
def lengthOfLIS(self, nums: List[int]) -> int:
    # n = len(nums)
    # f = [0] * n
    # for i in range(n):
    #     for j in range(i):  # 遍历i之前的数
    #         if nums[j] < nums[i]:
    #             f[i] = max(f[i], f[j])
    #     f[i] += 1
    # return max(f)
    n = len(nums)
    @cache
    def dfs(i):
        res = 0
        for j in range(i):
            if nums[j] < nums[i]:
                res = max(res, dfs(j))
        return res + 1
    return (max([dfs(i) for i in range(n)]))
```

**19. 删除链表的倒数第 N 个结点**
方法：前后指针
```python
def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
    dummy = ListNode(next=head)
    right = dummy
    for _ in  range(n):
        right = right.next
    left = dummy
    while right.next:  # right.next is not None
        left = left.next
        right = right.next
    # 此时left指向倒数第N+1个
    # 删除left.next（倒数第N个结点）
    left.next = left.next.next
```


