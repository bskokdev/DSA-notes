- We use **seen set or Boolean[]** to detect already visited nodes and to prevent cycles in **undirected graphs**
- However, in a **directed graph** we need to use **path backtracking** to check whether the current node is part of the current path and therefore would create a cycle
```python
visited, path = set(), set()

# check cycle in a directed graph
def has_cycle(node):
	if node in path:
		return True

	if node in visited:
		return False
	
	visited.add(node)
	# Path backtracking
	path.add(node)
	for nei in g[node]:
		if has_cycle(nei):
			return True
	path.remove(node)
	return False
```
