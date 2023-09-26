**Problem Statement:**
- Find triplets in an integer array which sums up to 0.
- **The result list must not contain duplicates**.

**Approach & pattern used:**
- First sort the input list so I can use **two pointers two sum approach** on the sorted list.
- For each number in the sorted list I try to find a pair of numbers which sum up to `-num`.
	- If I find such pair, the sum of the triplet == 0.
- I also need to handle the duplicates:
	- `if i > 0 and nums[i] == nums[i-1]`:
		- This means there's a duplicate for the `i`.
	- `if left+1 < n and nums[left] == nums[left+1]`:
		- This means there's a duplicate for the `left`.
	- `if right-1 >= 0 and nums[right] == nums[right-1]`:
		- This means there's a duplicate for the `right`.

**Pseudocode:**

```python
def threeSum(self, nums: List[int]) -> List[List[int]]:
	n = len(nums)
	nums.sort()
	res = []
	for i, num in enumerate(nums):
		# Handle ith index duplicates
		if i > 0 and nums[i] == nums[i-1]:
			continue
		cur_target = -num
		left, right = i+1, n-1
		while left < right:
			cur_sum = nums[left] + nums[right]
			# Found a valid triplet
			if cur_sum == cur_target:
				res.append([num, nums[left], nums[right]])
				# Skip left index duplicates
				while (
					left+1 < n and
					nums[left] == nums[left+1]
				):
					left += 1
				# Skip right index duplicates
				while (
					right-1 >= 0 and
					nums[right] == nums[right-1]
				):
					right -= 1
			if cur_sum > cur_target:
				right -= 1
			else:
				left += 1
	return res
```

**Complexity Analysis:**

- Time: O(n^2) - n log n for the sort; n^2 for the 2 loops.
- Space: O(n) - The result list ((1/3 * n) * 3 -> n).

**Learnings:**

- When working with finding **pairs/triplets, so on** I can utilize the sorting and two pointers to find the solution.
- **In order to handle duplicates**:
	- check if the index is within bounds
	- Check either previous index or the next index for the same value:
		- `if i < n and nums[i] == nums[i+1]`
		- `if i > 0 and nums[i] == nums[i-1]`

**Next Steps:**

- For pairs, triplets, etc., try to utilize sorting and 2 pointers