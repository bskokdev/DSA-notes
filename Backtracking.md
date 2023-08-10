## General Overview
- Recursively generate all combinations, permutations etc.
- We need to traverse the input in the DFS function
	- **1D input** (string, nums array) - pass an index
	- **2D input** (matrix) - pass row, col
		- **Check for in bounds and seen coordinates**
- For the recursive function we need to define a **base-case**
```python
if i >= len(nums):
	return
if not in_bounds(row, col):
	return
if rem < 0:
	return
```
- Then we **iterate over the options** we have
	- This could be numbers 1-9, characters in a dictionary, positions in matrix
	- in 2D grid we can move by using the directions array
```python
directions = [[0,1], [1,0], [0,-1], [-1,0]]
def dfs(row, col, state):
	# .... logic
	for dx, dy in directions:
		r, c = row + dx, col + dy
		# ... logic
```
- We would **modify the state on each iteration** (via DFS call)
- We need to **revert the state** after each modification
	- Pop from an array
	- Remove last char from string
	- Mark unseen
Example:
```python
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        n = len(nums)
        # we move in the input by passing index i
        def dfs(i):
	        # base case
            if i == n:
                res.append(nums[:])
                return
			# iterate over the options we have
            for j in range(i, n):
	            # modify the state
                nums[i], nums[j] = nums[j], nums[i]
                dfs(i+1)
                # revert the modification
                nums[i], nums[j] = nums[j], nums[i]
        dfs(0)
        return res
```