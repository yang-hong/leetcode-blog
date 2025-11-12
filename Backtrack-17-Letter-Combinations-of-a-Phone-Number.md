
## 🧩 Problem
https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/

## 💭 My thinking process
We first create a number_to_letters map ["2":"abc"], and we call backtrack(start index, path). Depth of the recurtion is length of the digits. And for loop represent each letter for that digit. For each letter mapped to digits[index], append it and recurse to next digit. So we need digits[curr_index] and number_to_letters[curr_number]

## 💡 Things I have challenges with
1. if it is string, do not need to do path.pop

## 🧠 Code
```
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []
            
        res = []
        number_to_letters = {
            "2" : "abc",
            "3" : "def",
            "4" : "ghi",
            "5" : "jkl",
            "6" : "mno",
            "7" : "pqrs",
            "8" : "tuv",
            "9" : "wxyz"
        }

        def backtrack(curr_index, path):
            if curr_index == len(digits):
                res.append(path[:])
                return
            
            curr_number = digits[curr_index]
            curr_letters = number_to_letters[curr_number]
            
            for curr_letter in curr_letters:
                backtrack(curr_index + 1, path + curr_letter)
            
        backtrack(0, "")
        return res
```

## 📈 Complexity
| Component           | Complexity | Explanation                           |
| ------------------- | ---------- | ------------------------------------- |
| **Time**            | O(n × mⁿ)  | `mⁿ` combinations, each built in O(n) |
| **Space**           | O(n × mⁿ)  | Result storage + recursion            |
| **Recursion depth** | O(n)       | One level per digit                   |
