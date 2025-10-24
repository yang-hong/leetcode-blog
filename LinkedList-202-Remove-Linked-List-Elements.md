## 🧩 Problem
https://leetcode.com/problems/design-linked-list/

## 💭 My thinking process
loop through the linkedlist node value, if value = val, then curr.node.next = curr.node.next.next. Use dummy node to save the head node, return the origional head node (dummy.next)

## 💡 Things I have challenges with
1. out of boundary. If we have curr.next.next, for while loop, it needs to be while curr.next
2. If curr.next.val == val, we perform the operation, else we move the curr pointer. This is to make sure after operation is done, we don't accidently skip the next node. 

## 🧠 Code
```
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        #loop through the linkedlist node value, if value = val, then curr.node.next = curr.node.next.next
        dummy = ListNode(0)
        dummy.next = head
        curr = dummy
        while curr.next:
            if curr.next.val == val:
                curr.next = curr.next.next
            else: 
                curr = curr.next
        
        return dummy.next
```

## 📈 Complexity
Time Complexity	Each node is visited exactly once → O(n)	O(n)
Space Complexity	Only uses a few pointers (dummy, curr) → constant space	O(1)