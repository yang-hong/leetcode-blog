## 🧩 Problem
https://leetcode.com/problems/intersection-of-two-linked-lists/

## 💭 My thinking process
join the two lists, it will enter the intersection at the same time

## 💡 Things I have challenges with
1. Both walk a + b + c nodes → same distance. That’s why they meet exactly at the intersection node.

## 🧠 Code
```
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        #join the two lists, it will enter the intersection at the same time
        if not headA or not headB:
            return None
        
        pA, pB  = headA, headB
        while pA != pB:
            pA = pA.next if pA else headB
            pB = pB.next if pB else headA
        return pA

```