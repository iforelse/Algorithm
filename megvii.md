## 题库链接:>https://codetop.cc/home>
### 01 反转链表 II 
- <https://leetcode.cn/problems/reverse-linked-list-ii>
- 首先学会[反转链表](https://leetcode.cn/problems/reverse-linked-list/description/)
  - ```python
    # Definition for singly-linked list.
    # class ListNode:
    #     def __init__(self, val=0, next=None):
    #         self.val = val
    #         self.next = next
    class Solution:
        def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
            pre = None
            cur = head
            # nxt = None
            while cur:
                nxt = cur.next
                cur.next = pre
                pre = cur
                cur = nxt
            return pre
        ```
  - 反转链表 II 的步骤:
    1. 反转子的链表
