## 🧩 Problem
https://leetcode.com/problems/evaluate-reverse-polish-notation/

## 💭 My thinking process
Create a stack. Loop through each c in string. If it is "+", "-", "*", "/", we pop last values from stacks and perform the operation and put back. Return the first element of stack

## 💡 Things I have challenges with
1. "//" is round down and int. "/" is round toward zero. "int(/)"  is round toward zero and int
2. Order of the operation. For // and -, need to use second popped value minus first popped value

## 🧠 Code
```
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []

        for c in tokens:
            if c == "+":
                stack.append(stack.pop() + stack.pop())
            elif c == "-":
                first = stack.pop()
                second = stack.pop()
                stack.append(second - first)
            elif c == "*":
                stack.append(stack.pop() * stack.pop())
            elif c == "/":
                first = stack.pop()
                second = stack.pop()
                stack.append(int(second / first))
            else:
                stack.append(int(c))
        
        return stack[0]

```