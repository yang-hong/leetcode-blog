## 🧩 Problem
https://leetcode.com/problems/network-delay-time/

## 💭 My thinking process
Dijkstra is from a start point to the all point, what is the shorted path. It is a directed graph. For prim, it is from any unreached point, the shorted path to reach the reached point. The result is a tree. It is undirected. prim是求 非访问节点到最小生成树的最小距离，而 dijkstra是求 非访问节点到源点的最小距离。
Build adjacency list(graph), heap, visited set(), and shortest {}. Put the starting point (time, node) to minHeap and put shortest[node] = time. For neighbor of this node, push to the minheap, while pushing, time = time + weight to make sure it has the cumulated weights. When the len(shorted) == n, meaning that we have visited all points, we return the max value from shortest 

## 💡 Things I have challenges with

## 🧠 Code
```
class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        #build the graph first
        graph = defaultdict(list)
        for u,v,w in times:
            graph[u].append((v,w))
        
        #min heap to always process the shortest path first
        heap = [(0,k)]
        visited = set()
        shortest = {}

        #Dijkstra’s algorithm
        while heap:
            time, node = heapq.heappop(heap)
            if node in visited:
                continue
            visited.add(node)
            shortest[node] = time

            #Explore neighbors
            for neighbor, weight in graph[node]:
                if neighbor not in visited: 
                    heapq.heappush(heap, (time + weight, neighbor))
        
        #Did we reach all nodes?
        if len(shortest) != n:
            return -1
        return max(shortest.values())
        

```

## 📈 Complexity
⏱ Time Complexity
O(E log V)

Why:

Each edge can be relaxed once → O(E)

Each heap push/pop costs O(log V)

Total heap operations are bounded by the number of edges

🧠 Space Complexity (for completeness)
O(E + V)

Adjacency list: O(E)

Distance array: O(V)

Min-heap: up to O(E) entries