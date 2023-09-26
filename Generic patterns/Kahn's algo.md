- Used to topologically sort mainly a directed graph (**can be used also on undirected**).
- We need to keep an indegree array/dictionary to count how many nodes point to node at indegree[node].
- We only add nodes with indegree == 0 (for directed graphs) or indegree == 1 (for directed graphs) to the queue.
```python
    def findOrder(self, numCourses, prerequisites):
        n = numCourses
        # node value: [0, n-1]
        graph = defaultdict(list)
        in_degree = [0] * n
        for pre in prerequisites:
            graph[pre[1]].append(pre[0])
            in_degree[pre[0]] += 1
            
        q = deque()
        for node in range(n):
            if in_degree[node] == 0:
                q.append(node)

        res = []
        while q:
            cur = q.popleft()
            res.append(cur)
            in_degree[cur] -= 1
            for nei in graph[cur]:
                in_degree[nei] -= 1
                if in_degree[nei] == 0:
                    q.append(nei)

        # check for a cycle
        if len(res) != n:
            return []
        return res
```
- It is often used to solve dependency questions (1 actions depends on other action etc.) 