## 题库链接:>https://codetop.cc/home>
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

### 04 [环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/description/)
- 简单思路：遍历，将值存入set()，检查cur是否在set中。
'''python
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
'''
