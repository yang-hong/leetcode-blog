## 🧩 Problem
https://leetcode.com/problems/design-linked-list/

## 💭 My thinking process
Construct a ListNode class with val and next pointer. Use while loop and for loop to find the right get/insert/delete position and insert the newly created Node, and connect this node to the existing linkedlist

## 💡 Things I have challenges with
1. There are many corner cases, so we need to introduce another variable: size to record the current linked list size. We need to make sure the inserting index is larger than 0 and less or equal to the current size. Also, if size is 0, self.tail = node. 

2. The time complexity is large if we don't introduce tail pointer. If we don't introduce tail pointer, every time we insert to tail, we need to loop through till the end. 

## 🧠 Code
```
class MyLinkedList:
    class Node:
        def __init__(self, val, next=None):
            self.val = val
            self.next = next

    def __init__(self):
        self.head = None
        self.tail = None  # ✅ NEW tail pointer
        self.size = 0

    def get(self, index: int) -> int:
        if index < 0 or index >= self.size:
            return -1
        curr = self.head
        for _ in range(index):
            curr = curr.next
        return curr.val

    def addAtHead(self, val: int) -> None:
        node = self.Node(val, self.head)
        self.head = node
        if self.size == 0:       # ✅ if empty, tail also points to new node
            self.tail = node
        self.size += 1

    def addAtTail(self, val: int) -> None:
        node = self.Node(val)
        if self.size == 0:
            self.head = node
            self.tail = node
        else:
            self.tail.next = node
            self.tail = node     # ✅ move tail forward
        self.size += 1

    def addAtIndex(self, index: int, val: int) -> None:
        if index > self.size:
            return
        if index <= 0:
            self.addAtHead(val)
            return
        if index == self.size:
            self.addAtTail(val)
            return

        curr = self.head
        for _ in range(index - 1):
            curr = curr.next
        node = self.Node(val, curr.next)
        curr.next = node
        self.size += 1

    def deleteAtIndex(self, index: int) -> None:
        if index < 0 or index >= self.size:
            return
        if index == 0:
            self.head = self.head.next
            if self.size == 1:       # ✅ update tail if deleting only node
                self.tail = None
        else:
            curr = self.head
            for _ in range(index - 1):
                curr = curr.next
            curr.next = curr.next.next
            if index == self.size - 1:  # ✅ deleted last node → move tail back
                self.tail = curr
        self.size -= 1
```

## 📈 Complexity
With a tail pointer (head + tail + size)

get(index): O(n)

addAtHead(val): O(1)

addAtTail(val): O(1) ✅ (no traversal)

addAtIndex(index, val): O(n)

deleteAtIndex(index): O(n) (need predecessor in singly list)

Space: O(n)