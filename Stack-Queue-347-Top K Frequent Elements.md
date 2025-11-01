## 🧩 Problem
https://leetcode.com/problems/top-k-frequent-elements/

## 💭 My thinking process
Because we want top K, so we use min heap to pop min each time, and what's left are top K. Also, because we are using min Heap, the top of heap (heap[0]) is always smallest. Everytime we pop, we pop from top (the smallest). In the remaining heap, the top is also smallest, so in the end array, we want use [::-1] to reverse it. Use dictionary to store (value: frequency)

## 💡 Things I have challenges with
1. for num in arrayList.keys(): -> heapq.heappush(heap, [arrayList[num], num])
2. return [heapq.heappop(heap)[1] for _ in range(len(heap))]
3. Python default is minHeap, for maxHeap, need to use negate value
4. Minheap stores min at top(heap[0]), and pop at the top. Heap is a special kind of deque. Deque is double ended but minheap is one end. Deque popleft() is like deque[0] (pop the first element)
5. Peek or pop from top of heap is o(1) and pop/insert is o(logn) and heapify is o(n)

## 🧠 Code
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()

        for i in range(len(nums)):
            left, right = i + 1, len(nums) - 1

            #skip outter loop duplicate
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            while left < right:
                total = nums[left] + nums[right] + nums[i]
                
                if total > 0:
                    right -= 1
                elif total < 0:
                    left += 1
                else:
                    res.append([nums[i], nums[left], nums[right]])
                    left += 1
                    right -= 1
                    while left < right and nums[left] == nums[left - 1]:
                        left += 1
                    while left < right and nums[right] == nums[right + 1]:
                        right -= 1
        
        return res
```

## 📈 Complexity
| Step                            | Operation                                  | Count    | Cost per op      | Total          |
| ------------------------------- | ------------------------------------------ | -------- | ---------------- | -------------- |
| ① Count frequencies (`Counter`) | Traverse `nums` once                       | `n`      | O(1)             | **O(n)**       |
| ② Heap push/pop loop            | One iteration per **distinct** element `m` | `m`      | O(log k)` (max)` | **O(m log k)** |
| ③ Pop results (≤ k elements)    | k                                          | O(log k) | **O(k log k)**   |                |

T(n)=O(n)+O(mlogk)+O(klogk) -> T(n)=O(nlogk)​

| Source        | Space |
| ------------- | ----- |
| Frequency map | O(m)  |
| Heap          | O(k)  |
| Output array  | O(k)  |

O(m+k) = O(k)