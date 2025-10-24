## 🧩 Problem
https://leetcode.com/problems/reverse-linked-list/

## 💭 My thinking process
Use prev and curr pointer to reverse each node while loop through the whole linked list.

## 💭 Things I have challenges with
1. return type should be prev instead of curr because at the end of while loop, curr is already curr.next
## 🧠 Code
```
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        curr = head

        while curr:
            tmp = curr.next
            curr.next = prev
            prev = curr
            curr = tmp
        
        return prev
```

## 📈 Complexity
Time Complexity	We visit each node exactly once, performing O(1) work per node.	O(n)
Space Complexity	We only use a few extra pointers: prev, curr, nxt.	O(1)