**Problem Statement:**
- This problem asks me to find the the distance of the nearest cell with `value == 0` in a 2d grid

**Approach & pattern used:**
- My initial though was to iterate over the grid and run BFS from cells which are not == 0. This wouldn't be optimal, but should work.
- Better approach is to use **Multisource BFS** from 0 cells.
- This means I first find cells with `value == 0` and store them in a queue, also mark these cells in the result grid as distance 0 as they are already zeros
- Then do the **Level Order BFS** on the queue.
	- for each adj. cell I check if it's within bounds & `res[new_row][new_col] == -1` => this takes care of our seen grid/set and allows us to explore non-zero cells at the same time.
		- if the conditions are true, update result grid for the adjanced coordinates:
			- `res[new_row][new_col] = level`
			- and append to the queue in case other non-zero cells are present.

**Pseudocode:**

```python
m, n = len(matrix), len(matrix[0])
queue = deque()
res = [[-1] * n for _ in range(m)]

# Fill the queue
for r in range(m):
	for c in range(n):
		if matrix[r][c] == 0:
			q.append((r, c))
			res[r][c] = 0

# Move in 4 directions in the grid
directions = [[0,1], [1,0], [0,-1], [-1,0]]
level = 0
while q:
	level += 1
	# len(q) == size of current level
	for _ in range(len(q)):
		row, col = q.popleft()
		for dx, dy in directions:
			new_r, new_c = row + dx, col + dy
			# Check grid bounds & if it has been seen yet
			if (0 <= new_r < m and 0 <= new_c < n and
				res[new_r][new_c] == -1):
				# Add to queue in case of adj non-zero nodes 
				q.append((new_r, new_c))
				# Set the level to be the distance
				res[new_r][new_c] = level
return res
```

**Complexity Analysis:**

- Time: O(m * n) - I need to traverse the entire grid.
- Space: O(m * n) - I store additional result grid.

**Learnings:**

- I used **Multisource BFS** pattern
	- This doesn't have to be used only on nodes with values we care about but rather on nodes we don't care about. I don't put cells != 0 to the queue here and rather store cells where value == 0 and run BFS from them.

**Next Steps:**

- Be careful with choosing the correct type of node to run the BFS from.
- **Multisource BFS** can be used on many problems which require shortest number of steps in something.
