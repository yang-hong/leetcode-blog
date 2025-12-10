## 🧩 Problem
https://leetcode.com/problems/all-paths-from-source-to-target/description/

## 💭 My thinking process
Have res array and path array. First call dfs with first node, and put the node to path. Second keep doing dfs search for this node's neighbors, until the node equals the length of graph (which equals to the value of target node), we append path to result, once we exist one level of recursion, pop the value from path to do backtrack

## 💡 Things I have challenges with
1. path.copy()
2. path.pop()
3. Since index represent node value, length of graph is the target node value

## 🧠 Code
```
class Solution:
    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:
        res = []
        path = []

        def dfs(node):
            path.append(node)

            if node == len(graph) - 1:
                res.append(path.copy())
            else:
                for neighbor in graph[node]:
                    dfs(neighbor)

            path.pop()

        dfs(0)
        return res
```

## 📈 Complexity
Since the graph is a DAG, in the worst case it may contain an exponential number of paths.
DFS explores all of them, and copying each full path costs O(n).
Therefore the time complexity is O(2ⁿ), and the space complexity is O(n) due to recursion depth.