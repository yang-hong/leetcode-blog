## 🧩 Problem
https://leetcode.com/problems/course-schedule-ii/description/

## 💭 My thinking process
Have res[], inDegree[] that store 入度for each course number (no need to uss map. index represents course number), dictionary graph to store source: [dest course, dest course] ({0: [1, 2], 1: [3], 2: [3]}), and deque() for bfs. Loop through each prerequisites to form the graph and inDegree. Loop through inDegree to find the first src course with 0 indegree and append to queue to perform bfs. For dest in this source, minus inDegree. If you see a new course inDegree becomes 0, meaning that there is no prerequisite for this course, we can take that course. return res until len of res equal to numCourses

## 💡 Things I have challenges with
1. Adjacency list: graph[src].append(dest)
defaultdict(<class 'list'>, {0: [1, 2], 1: [3], 2: [3]})

## 🧠 Code
```
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        res = []
        inDegree = [0] * numCourses
        graph = defaultdict(list)
        queue = deque()

        for dest, src in prerequisites:
            graph[src].append(dest)
            inDegree[dest] += 1
        
        print(graph)

        for i in range(len(inDegree)):
            if inDegree[i] == 0:
                queue.append(i)
        
        while queue:
            course = queue.popleft()
            res.append(course)

            for neighbor in graph[course]:
                inDegree[neighbor] -= 1
                if inDegree[neighbor] == 0:
                    queue.append(neighbor)

        if len(res) == numCourses:
            return res
        else: 
            return []

```

## 📈 Complexity
O(V + E)

Why:

Building the graph takes O(E)

Each node is processed once → O(V)

Each edge is visited once when reducing indegrees → O(E)

🧠 Space Complexity
O(V + E)

Adjacency list: O(E)

Indegree array / visited states: O(V)

Queue / recursion stack: O(V)