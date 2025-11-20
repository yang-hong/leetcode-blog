## 🧩 Problem
https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/

## 💭 My thinking process
First, create a dictionary to store the last occurance of each character. Loop through each character, and update the end variable with the current maximum of the last occurance of each character seen. If i == end, meaning we have reach the farest place where it has duplicated characters, we can safely cut. and then update the start index to the end + 1

## 💡 Things I have challenges with
1. for i, ch in enumerate(s):
        last_occurrence[ch] = i

## 🧠 Code
```
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        last_occurrence = {}  # 存储每个字符最后出现的位置
        for i, ch in enumerate(s):
            last_occurrence[ch] = i

        result = []
        start = 0
        end = 0
        for i, ch in enumerate(s):
            end = max(end, last_occurrence[ch])  # 找到当前字符出现的最远位置
            if i == end:  # 如果当前位置是最远位置，表示可以分割出一个区间
                result.append(end - start + 1)
                start = i + 1

        return result
```

## 📈 Complexity
Time: O(n)
Space: O(n)