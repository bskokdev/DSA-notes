## Multi-source BFS
- We first push nodes to the queue based on a condition
```python
q = deque()
for row in range(len(grid)):
	for col in range(len(grid[0])):
		if grid[row][col] == 1:
			q.append((row, col))
# ... classic BFS/level-order BFS
```
- This is used when we need to run BFS from multiple source nodes typically in a matrix graph (https://leetcode.com/problems/rotting-oranges/)
- Hint could be that something spreads in the array (fire etc.) per time unit (=level)
