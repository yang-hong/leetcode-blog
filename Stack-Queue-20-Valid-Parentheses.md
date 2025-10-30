## 🧩 Problem
https://leetcode.com/problems/implement-stack-using-queues/

## 💭 My thinking process
Have a stack and diectionary. For dictionary, key is closing brackets and value is open brackets. For each char in string, if it is open, we put to stack. If it is close, we get the last value from stack and comopare with the value from dictionary. If it is the same, continue and pop the top stack until stack is empty

## 💡 Things I have challenges with
1. Get the top element from stack but without poping: stack[-1]
2. Check if stack is empty: len(stack) == 0
3. Corner case: if first element is close, we return False directly. Or if there are 2 close that are close to each other, we return False

## 🧠 Code
```
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        hashmap = {')':'(', ']':'[', '}':'{'}

        for c in s:
            if c in '[{(':
                stack.append(c)
            elif c in ']})':
                if not stack:
                    return False
                top = stack[-1]
                if top == hashmap[c]:
                    stack.pop()
                else:
                    return False
        
        return len(stack) == 0

```
