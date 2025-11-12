
## 🧩 Problem
https://leetcode.com/problems/combinations/description/

## 💭 My thinking process
We have a backtrack inner function with starting position. For i in range all of the numbers, we append the number and keep going one level down by calling backtrack(i + 1) until the length of path equals k, we return the recurtion and do the shalow copy of the path to result. 

## 💡 Things I have challenges with
1. Always do path.pop()
2. Diff between shallow and deep copy
| Operation        | Level         | Shared Objects?      | Common Syntax      | When to Use                 |
| ---------------- | ------------- | -------------------- | ------------------ | --------------------------- |
| `b = a`          | None          | Everything           | `b = a`            | Reuse same object           |
| **Shallow copy** | Outer only    | Inner objects shared | `a[:]`, `a.copy()` | Flat / simple structures    |
| **Deep copy**    | Outer + Inner | Nothing shared       | `copy.deepcopy(a)` | Nested / complex structures |
3. When you have a container object — like a list, dict, set, or class instance — the items inside it are called its inner objects (or contained objects).
4. int, float, str, tuple, inner object does not matter, meaning when changing those with shallow copy, it won't change. Only list, dict, set, object are mutable

## 🧠 Code
```
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        res = []
        path = []

        def backtrack(start):
            if len(path) == k:
                res.append(path[:])
                return
            
            for i in range(start, n + 1):
                path.append(i)
                backtrack(i + 1)
                path.pop()
        
        backtrack(1)
        return res
```

## 📈 Complexity
| Component             | Complexity         | Explanation                         |
| --------------------- | ------------------ | ----------------------------------- |
| **Time**              | **O(k × C(n, k))** | Each combination costs O(k) to copy |
| **Space**             | **O(k × C(n, k))** | For storing all results             |
| **Auxiliary (stack)** | **O(k)**           | Recursion depth                     |
