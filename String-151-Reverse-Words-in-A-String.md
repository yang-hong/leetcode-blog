## 🧩 Problem
https://leetcode.com/problems/reverse-words-in-a-string/

## 💭 My thinking process
Remove the front and end space. Reverse the whole string. For each char in each words, reverse char

## 💡 Things I have challenges with
1. Simple solution is to convert string to array using s.split(), that is split by space. Each array value is a word. For that array, reverse each words. 
2. Convert from array to string by using " ".join(words)

## 🧠 Code
```
class Solution:
    def reverseWords(self, s: str) -> str:
        words = s.split()

        words.reverse()

        return " ".join(words)
```

```
class Solution:
    def reverseWords(self, s: str) -> str:
        # 将字符串拆分为单词，即转换成列表类型
        words = s.split()

        # 反转单词
        left, right = 0, len(words) - 1
        while left < right:
            words[left], words[right] = words[right], words[left]
            left += 1
            right -= 1

        # 将列表转换成字符串
        return " ".join(words)

```