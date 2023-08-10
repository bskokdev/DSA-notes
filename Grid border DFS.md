- Useful for surrounded portions of a graph (matrix representation)
- https://leetcode.com/problems/surrounded-regions/
- https://leetcode.com/problems/pacific-atlantic-water-flow/
- We start our DFS on edge nodes in the grid and then
```python
# first & last row
for i in range(n):
	if board[0][i] == "O":
		dfs(0, i)

	if board[m-1][i] == "O":
		dfs(m-1, i)

# first & last col
for i in range(m):
	if board[i][0] == "O":
		dfs(i, 0)

	if board[i][n-1] == "O":
		dfs(i, n-1)
```
