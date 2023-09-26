## Overview
This pattern is useful whenever the values of nodes are not really important and rather some property of the graph has to be discovered.

## Idea
The idea is rather simple
- Iterate over each node in the graph
	- Do DFS/BFS on every `ith` node
		- Check if a property of neighbour nodes is OK

## Example code solution
![[Pasted image 20230913005710.png]]
```python
    def isBipartite(self, graph: List[List[int]]) -> bool:
        colors = {}
        n = len(graph)
        # We loop over every node in the graph
        for node in range(n):
          if node not in colors:
            colors[node] = 1
		  # Do the BFS on the the ith node
          q = deque([node])
          while q:
            cur = q.popleft()
            # Check the correct neighbour nodes' property
            for adj in graph[cur]:
              if adj not in colors:
                colors[adj] = -colors[cur]
                q.append(adj)
              if colors[adj] == colors[cur]:
                return False
        return True
```