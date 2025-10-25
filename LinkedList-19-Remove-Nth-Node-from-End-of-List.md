## 🧩 Problem
https://leetcode.com/problems/remove-nth-node-from-end-of-list/

## 💭 My thinking process
one fast pointer and one slow pointer, fast moves to n + 1 first, and then slow and fast move together until fast reaches to the end

## 💡 Things I have challenges with
1. Move fast n + 1 steps ahead to make sure slow lands exactly before the node to delete
2. put fast, slow point to dummy instead of head since we are moving n + 1 steps instead of n to prevent out of boundary
3. When deleting from a linked list, always make sure the slow pointer lands on the node before the one to remove — and a dummy node guarantees that node always exists

## 🧠 Code
```
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        fast, slow = dummy, dummy

        for _ in range(n + 1):
            fast = fast.next
        
        while fast:
            fast = fast.next
            slow = slow.next
        
        slow.next = slow.next.next
        return dummy.next

```



## 📈 Complexity
Time	Traverse the list once using two pointers	O(n)
Space	Only a few extra pointers	O(1)