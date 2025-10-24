## 🧩 Problem
https://leetcode.com/problems/swap-nodes-in-pairs/

## 💭 My thinking process
have pre pointer points to head and curr points to head.next, and do the swap

## 💡 Things I have challenges with
1. There are 2 ways, if use recursion, need to have next = head.next.next to record the next head of the recursion
2. Recursion can be called as pre.next = self.swapPairs(next)
3. If using iterative approach, need to store curr.next.next as tmp1 variable as wel. Draw the picture

## 🧠 Code
```
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:

        if head is None or head.next is None:
            return head
        
        pre = head
        curr = head.next
        next = head.next.next

        curr.next = pre
        pre.next = self.swapPairs(next)

        return curr

```

```
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy_head = ListNode(next=head)
        current = dummy_head
        
        # 必须有cur的下一个和下下个才能交换，否则说明已经交换结束了
        while current.next and current.next.next:
            temp = current.next # 防止节点修改
            temp1 = current.next.next.next
            
            current.next = current.next.next
            current.next.next = temp
            temp.next = temp1
            current = current.next.next
        return dummy_head.next

```

## 📈 Complexity
| Metric                           | Value | Why                      |
| -------------------------------- | ----- | ------------------------ |
| **Time Complexity**              | O(n)  | Each node processed once |
| **Space Complexity (recursive)** | O(n)  | Function call stack      |
| **Space Complexity (iterative)** | O(1)  | Only pointers used       |
