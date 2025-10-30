## 🧩 Problem
https://leetcode.com/problems/implement-stack-using-queues/

## 💭 My thinking process
Everytime we push a new element into queue, rotate the previous elements behind new element

## 💡 Things I have challenges with
1. Do operation under push 
2. queue[0] returns the top of queue, queue[-1] returns the last of queue
3. Check empty: if not self.queue

## 🧠 Code
```
class MyStack:

    def __init__(self):
        self.queue = deque()

    def push(self, x: int) -> None:
        self.queue.append(x)
        #rotate the previous elements behind x
        for _ in range(len(self.queue) - 1):
            self.queue.append(self.queue.popleft())

    def pop(self) -> int:
        return self.queue.popleft()

    def top(self) -> int:
        return self.queue[0]

    def empty(self) -> bool:
        return not self.queue

```

## 📈 Complexity
| Operation   | Time Complexity | Explanation                          |
| ----------- | --------------- | ------------------------------------ |
| **push(x)** | O(n)            | Need to rotate the queue (n−1 moves) |
| **pop()**   | O(1)            | Just `popleft()`                     |
| **top()**   | O(1)            | Peek front element                   |
| **empty()** | O(1)            | Check queue emptiness                |
