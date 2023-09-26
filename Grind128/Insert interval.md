**Problem Statement:**
- Given list of intervals sorted by starts, insert a given interval so that the initial list stays sorted and doesn't contains overlap

**Approach & pattern used:**
- I used `current working interval pattern`.
	- This is basically having an interval outside of the iteration and I update it on a certain condition.
- 2 conditions I care about are:
	- There is **not** an overlap:
		- Here I insert the `working` interval to the result
		- And update the `working` interval to `intervals[i]`
	- There is an overlap:
		- Merge `intervals[i]` & `working` interval:
			- `working[0] = min(working[0], intervals[i][0])`
			- `working[1] = max(working[1], intervals[i][1])`
	- If none of these conditions is valid:
		- Insert the `intervals[i]` to the result

**Pseudocode:**

```python
def insert(intervals: List[List[int]], new: List[int]):

	res = []
	working = new

	for interval in intervals:
		# We are fine to insert here
		if interval[0] > working[1]:
		   res.append(working)
		   cur = interval
		# There's an overlap
		elif working[0] <= interval[1]:
			working[0] = min(working[0], interval[0])
			working[1] = max(working[1], interval[1])
		else:
			res.append(interval)
			
	# In case we didn't insert prior
	res.append(working)
	return res
```

**Complexity Analysis:**

- Time: O(n) - I just look over the intervals.
- Space: O(N) - Extra result list space.

**Learnings:**

- I used **working interval pattern**
	- This simplifies merge operations
- Whiteboarding interval problems helps a lot

**Next Steps:**

- In intervals I only care about sorting of the list or I extract logic to the working interval