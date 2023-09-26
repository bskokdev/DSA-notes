**Problem Statement:**
- Given a node of a graph, return it's deep copy

**Approach & pattern used:**
- **For deep copies think of using hash map**
	- Map old values to new ones
- In case of the graph I need to handle also neighbours of newly created nodes and be careful of **null values**.
- So in this problem I just traverse the graph and populate the mapping.

**Pseudocode:**

```python
def cloneGraph(self, node: Node) -> Optional[Node]:
	if not node:
		return None
		
	# Store old to new pairs
	old_new = {}
	
	# Run BFS
	q = deque([node])
	while q:
		cur_node = q.popleft()
		if cur_node not in old_new:
			old_new[cur_node] = Node(cur_node.val)
			
		for nei in cur_node.neighbors:
			if nei not in old_new:
				old_new[nei] = Node(nei.val)
				q.append(nei)
			# Don't forget neighbors of current node's copy
			old_new[cur_node].neighbors.append(old_new[nei])
			
	return old_new[node]
```

**Complexity Analysis:**

- Time: O(V + E) - BFS visits all nodes and edges.
- Space: O(V) - storing nodes in the mapping.

**Learnings:**

- **To create deep copies use mapping of old to new.**
- Be careful with the **null input**
- Time complexity of graph traversals in O(V+E)

**Next Steps:**

- When creating copies use a HashMap to create mappings.