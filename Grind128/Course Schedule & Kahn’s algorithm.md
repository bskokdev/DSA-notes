**Problem Statement:**
- Given a list of 2d arrays courses, where each course is denoted as ``[ai, bi]`` and indicates that you **must** take course `bi` first if you want to take course `ai`. Decide if you can finish all the courses.
- We can map this relation as a DAG: **(bi) ----> (ai)**

**Approach & pattern used:**
- I can do a topological sort and see if I can touch all the nodes in the graph. If not return False.
	- To do topological sort I use **Kahn's algorithm**:
		1. Build the graph from input
		2. Append nodes with indegree == 0 to the queue
		3. Do classic BFS & decrease neighbour nodes' indegree by 1
		4. `If indegree of neighbour node == 0` append to the queue

**Pseudocode:**

```python
def canFinish(n: int, prerequisites: List[List[int]]):
	# 1. Build the graph and indegree
	graph = defaultdict(list)
	in_degree = [0] * n
	for a, b in prerequisites:
		graph[b].append(a)
		in_degree[a] += 1

	# 2. Append nodes with indegree == 0 to the queue
	q = deque()
	for i in range(n):
		if in_degree[i] == 0:
			q.append(i)

	# 3. BFS with adj indegree decrement step
	completed = 0
	while q:
		cur_node = q.popleft()
		completed += 1
		for adj in graph[cur_node]:
			in_degree[adj] -= 1
			if in_degree[adj] == 0:
				q.append(adj)
				
	# 4. Check if completed == original nodes count
	return completed == n
```

**Complexity Analysis:**

- Time: O(V + E) 
	- In the worst case I go over all vertices and edges 
- Space: O(n) - Storing graph & indegree array.

**Learnings:**

- I do topological sort using Kahn's algorithm
	- If I cared about the actual values I would add `cur_node` to `completed = []` list
- I can use Kahn's algorithm to detected a cycle in a **directed graph** (completed != expected)
- **I can also use Kahn's algorithm for an undirected graph to find the leaf nodes.**

**Next Steps:**

- Apply Kahn's algorithm if I need topological ordering of a graph
- Try to apply it when I need to access leaf nodes in the graph.