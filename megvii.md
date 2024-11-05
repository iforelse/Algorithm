## 题库链接:<https://codetop.cc/home>
### 01 反转链表 II <https://leetcode.cn/problems/reverse-linked-list-ii>
- 首先学会[反转链表](https://leetcode.cn/problems/reverse-linked-list/description/)
  - 思路：
    - 需要3个变量：pre, cur, nxt
    - 逐个节点反转，返回pre（指向原本的最后一个节点，即现在的头节点）
  - 代码：
    ```python
    # Definition for singly-linked list.
    # class ListNode:
    #     def __init__(self, val=0, next=None):
    #         self.val = val
    #         self.next = next
    class Solution:
        def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
            pre = None
            cur = head
            while cur:
                nxt = cur.next
                cur.next = pre
                pre = cur
                cur = nxt
            return pre
    ```
- 反转链表 II 的方法
  - 思路：
    - 首先，反转结束后，pre指向right，cur指向right+1
    - 因此，子链表反转后，让left.next指向cur，让left-1指向pre
  - 步骤：
    1. **设置哨兵** dummy指向head前一节点（防止left无上一个节点）
    2. **找到left-1位置** p0从dummy往后循环left-1次
    3. **反转子链表** 用pre,cur,nxt反转（循环right-left+1次）
    4. **整理**
        - left.next【p0.next.next】指向right+1【cur】
        - (left-1).next【p0.next】指向right【pre】
    5. **返回** dummpy.next
  - 代码：
  ```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
      def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
          # 设置哨兵
          dummy = ListNode(next=head)
          p0 = dummy
          for _ in range(left - 1):
              p0 = p0.next
          # 反转子链表
          pre = None
          cur = p0.next  # 子链表的head
          for _ in range(right - left + 1):  # cur从left遍历到right+1
              nxt = cur.next
              cur.next = pre
              pre = cur
              cur = nxt
          # 整理
          p0.next.next = cur
          p0.next = pre
          return dummy.next
  ```
  - 拓展：[K 个一组翻转链表](https://leetcode.cn/problems/lru-cache/description/)
### 02 LRU缓存机制 <https://leetcode.cn/problems/reverse-linked-list-ii> 【未写】
- 方法0：直接用python的collections.OrderedDict类
- 方法1：哈希表+双向链表（dict+含pre和nxt的类）
### 03 对角线遍历 <https://leetcode.cn/problems/diagonal-traverse/description/> 【只看了思路】
- 思路：按对角线条数索引：
  - ↗的：找到起始点，按顺序遍历
  - ↙的：找到其实点，按顺序遍历

### 04 环形链表 II <https://leetcode.cn/problems/linked-list-cycle-ii/description/>
- 简单思路：遍历，将值存入set()，检查cur是否在set中。
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node_set = set()
        cur = head
        while cur:
            if cur in node_set:
                return cur
            else:
                node_set.add(cur)
                cur = cur.next
        return None
```

### 05 全排列 <https://leetcode.cn/problems/permutations/description/>
- 思路：回溯[https://www.bilibili.com/video/BV1mY411D7f6]!
  - [image](https://github.com/user-attachments/assets/aa40c330-ba55-4bca-8afe-07e5f6c9ccc8)

### 06 子集 <https://leetcode.cn/problems/subsets/description/>
- 思路：回溯[https://www.bilibili.com/video/BV1mG4y1A7Gu]!
  - ![image](https://github.com/user-attachments/assets/fd169e1a-cef2-4111-b0aa-835088add209)


### 001 最长公共前缀 <https://leetcode.cn/problems/longest-common-prefix/description/>
- 暴力做法最简单
- 复杂度分析
  - 时间复杂度：O(mn)，其中 m 为 strs 的长度，n 为 strs 中最短字符串的长度。
  - 空间复杂度：O(1)。返回值不计入。
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        s0 = strs[0]
        for j, c in enumerate(s0):
            for s in strs:
                if j == len(s) or c != s[j]:
                    return s0[:j]
        return s0
```


### 99 环形数组中的第K个最大元素 <https://leetcode.cn/problems/kth-largest-element-in-an-array/description/>
- 方法：快速选择（基于快排原理）
- 思路：
  - 随机选择基准pivot
  - 将nums分到子列表big,equal,small
  - 根据k与len(子列表)的关系，递归或得到结果。
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        def quick_select(nums, k):
            # 随机选一个基准数
            pivot = random.choice(nums)
            big, equal, small = [], [], []
            for num in nums:
                if num > pivot:
                    big.append(num)
                elif num < pivot:
                    small.append(num)
                else:
                    equal.append(num)
            # 第k大在big中，递归划分
            if k <= len(big):
                return quick_select(big, k)
            # k在small中(k>=small的起始位置)
            if k > len(nums) - len(small):
                # 找small中的第k-xx大
                return quick_select(small, k - (len(nums) - len(small)))
            # k在equal中
            return pivot
            
        return quick_select(nums, k)
```


### 198打家劫舍
- 动态规划==》回溯
- 代码：简单实现==》catch数组缓存结果，节省计算
  - ![image](https://github.com/user-attachments/assets/912a6527-6823-4f57-96e9-8d4ecbed8278)




## 作业？
迷路的机器人 https://leetcode.cn/problems/robot-in-a-grid-lcci/description/
