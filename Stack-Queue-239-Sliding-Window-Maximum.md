## 🧩 Problem
https://leetcode.com/problems/sliding-window-maximum/

## 💭 My thinking process
Use queue to store the index from nums. There are 3 conditions to perform the operations, if the curr value is larger than queue[-1], remove all values form queue. If curr value is smaller than top of queue, append. If there is full window, remove left value out of window. Record max when first full window formed

## 💡 Things I have challenges with
[  LEFT  |  ...  |  RIGHT  ]
| Operation       | End affected          | Explanation                      |
| --------------- | --------------------- | -------------------------------- |
| `append(x)`     | ➡️ **Right end**      | Add to the **right** (tail)      |
| `appendleft(x)` | ⬅️ **Left end**       | Add to the **left** (head)       |
| `pop()`         | ⬅️ **Right end**      | Remove from the **right**        |
| `popleft()`     | ➡️ **Left end**       | Remove from the **left**         |
| `dq[-1]`        | **Rightmost element** | Last element (end you append to) |
| `dq[0]`         | **Leftmost element**  | First element (front)            |


nums = [1, 3, -1, -3, 5, 3, 6, 7]
k = 3

| i | nums[i] | Action                                                 | Deque (indexes) | Deque (values) | Current Max |
| - | ------- | ------------------------------------------------------ | --------------- | -------------- | ----------- |
| 0 | 1       | append(0)                                              | [0]             | [1]            | –           |
| 1 | 3       | pop(0) since 1 < 3 → append(1)                         | [1]             | [3]            | –           |
| 2 | -1      | append(2)                                              | [1, 2]          | [3, -1]        | **3**       |
| 3 | -3      | append(3)                                              | [1, 2, 3]       | [3, -1, -3]    | **3**       |
| 4 | 5       | pop(3), pop(2), pop(1) (since all smaller) → append(4) | [4]             | [5]            | **5**       |
| 5 | 3       | append(5)                                              | [4, 5]          | [5, 3]         | **5**       |
| 6 | 6       | pop(5), pop(4) (since 5<6) → append(6)                 | [6]             | [6]            | **6**       |
| 7 | 7       | pop(6) (6<7) → append(7)                               | [7]             | [7]            | **7**       |


## 🧠 Code
```
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        result = []
        dq = deque() #store indexes

        #remove smaller values from right
        for i in range(len(nums)):
            while dq and nums[dq[-1]] < nums[i]:
                dq.pop()
            
            dq.append(i)
        
            #remove left value if out of window
            if dq[0] <= i - k:
                dq.popleft()
        
            #record max when first full window formed
            if i >= k - 1:
                result.append(nums[dq[0]])
        
        return result
```

## 📈 Complexity
| Type                           | Complexity | Why                                         |
| ------------------------------ | ---------- | ------------------------------------------- |
| **Time**                       | **O(n)**   | Each element pushed and popped at most once |
| **Space**                      | **O(k)**   | Deque holds at most k elements at a time    |
| **Amortized cost per element** | **O(1)**   | Push once, pop once                         |
