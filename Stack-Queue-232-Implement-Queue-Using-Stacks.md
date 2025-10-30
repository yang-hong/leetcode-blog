## 🧩 Problem
https://leetcode.com/problems/implement-queue-using-stacks/description/

## 💭 My thinking process
Have two stack, one for in stack, other one for out stack. When push a value, push to in stack. WHen pop or peek, we need to first move the values from in stack to out stack and then perform the peek and pop

## 💡 Things I have challenges with
1. Two stack, in and out stack

## 🧠 Code
```
class MyQueue:
    def __init__(self):
        # stack used for push operations
        self.in_stack = []
        # stack used for pop/peek operations
        self.out_stack = []

    def push(self, x: int) -> None:
        # always push into in_stack
        self.in_stack.append(x)

    def pop(self) -> int:
        # ensure elements are in correct order
        self._move_in_to_out()
        return self.out_stack.pop()

    def peek(self) -> int:
        # ensure elements are in correct order
        self._move_in_to_out()
        return self.out_stack[-1]

    def empty(self) -> bool:
        # queue is empty if both stacks are empty
        return not self.in_stack and not self.out_stack

    def _move_in_to_out(self):
        # move all elements from in_stack to out_stack only when out_stack is empty
        if not self.out_stack:
            while self.in_stack:
                self.out_stack.append(self.in_stack.pop())


```

## 📈 Complexity
| Operation   | Worst Case | Amortized Case     | Explanation                                                                                                                                                            |
| ----------- | ---------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **push(x)** | O(1)       | O(1)               | Always just `append()` into `in_stack` → constant time                                                                                                                 |
| **pop()**   | O(n)       | **O(1) amortized** | Only when `out_stack` is empty, we move all elements from `in_stack` to `out_stack`. Each element is moved **once** in total across all operations, so amortized O(1). |
| **peek()**  | O(n)       | **O(1) amortized** | Same reasoning as `pop()` — the move only happens occasionally.                                                                                                        |
| **empty()** | O(1)       | O(1)               | Just a length or boolean check.                                                                                                                                        |
