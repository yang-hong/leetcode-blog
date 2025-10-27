## 🧩 Problem
https://leetcode.com/problems/happy-number/

## 💭 My thinking process
Loop through each digit and add them together. Once they equal to 1, we end the loop and return true

## 💡 Things I have challenges with
1. Use set to return False when there is endless loop
2. When calculating each new n, we need to have a nested loop while n > 0. When first digit is 0, means we run out of the digits, so ending the loop

## 🧠 Code
```
class Solution:
    def isHappy(self, n: int) -> bool:
        seen = set()

        while n > 1:
            #process the endless loop case
            if n in seen: 
                return False
            seen.add(n)

            total = 0
            while n > 0:
                digit = n % 10
                total += digit * digit
                n = n // 10
            
            n = total # reset n to new total after all the current digits are processed
        
        return True

```

## 📈 Complexity
Time	Process digits (O(log n)) for a constant number of transformations	O(log n)
Space	Constant-bounded set of seen numbers	O(1)