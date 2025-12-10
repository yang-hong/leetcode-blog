## 🧩 Problem
https://leetcode.com/problems/trapping-rain-water/

## 💭 My thinking process
For each width position, we find its max heights from left and max heights from right, whcih will form the maximum the water it can hold. And then, for each width positon, we can get the min of maxHeight and maxRight, which is to pick one way to hold the water, and minus its own height(which is the dips) to get the height difference, and then multiply by width. And we add to the total sum. To calculate the maxright and maxLeft, we can use double pointer to loop through from both left and right. We can also use monotonic stack

## 💡 Things I have challenges with

## 🧠 Code
```
class Solution:
    def trap(self, height: List[int]) -> int:
        leftheight, rightheight = [0]*len(height), [0]*len(height)

        leftheight[0]=height[0]
        for i in range(1,len(height)):
            leftheight[i]=max(leftheight[i-1],height[i])
        rightheight[-1]=height[-1]
        for i in range(len(height)-2,-1,-1):
            rightheight[i]=max(rightheight[i+1],height[i])

        result = 0
        for i in range(0,len(height)):
            summ = min(leftheight[i],rightheight[i])-height[i]
            result += summ
        return result
```

```
# 单调栈压缩版
class Solution:
    def trap(self, height: List[int]) -> int:
        stack = [0]
        result = 0
        for i in range(1, len(height)):
            while stack and height[i] > height[stack[-1]]:
                mid_height = stack.pop()
                if stack:
                    # 雨水高度是 min(凹槽左侧高度, 凹槽右侧高度) - 凹槽底部高度
                    h = min(height[stack[-1]], height[i]) - height[mid_height]
                    # 雨水宽度是 凹槽右侧的下标 - 凹槽左侧的下标 - 1
                    w = i - stack[-1] - 1
                    # 累计总雨水体积
                    result += h * w
            stack.append(i)
        return result
```

## 📈 Complexity
Time: O(n)
Space: O(n)