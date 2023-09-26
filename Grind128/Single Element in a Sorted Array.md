**Problem Statement:**
- A sorted array contains all elements twice expect for one which appears only once, find this element.

**Approach & pattern used:**
- Recognized binary search - I was taking look at `nums[mid] and adjanced ints at nums[mid-1] and nums[mid+1]`. While this is not completely wrong and the binary search can be done in this fashion, it becomes hard to understand later.
- Key observation in this problem is that if `mid` happens to be at an even index I need to check if `nums[mid+1] == nums[mid]`. This condition comes from the fact that the array is an **odd size if there's an extra element present**. This means that from the start if the pairs are in the array without an extra element `nums[odd_idx] == nums[odd_idx+1]` - `[1,1,2,2]`.
- If mid happens to be an odd index I do `mid -= 1` to make it even again. Then I check for the previous condition and can reduce the search space this way.
- if `nums[mid] != nums[mid+1]`
	- I know that the target element happens to be in the left subarray because the `odd, even pattern` is interrupted.
	- else we know it's in the right subarray because the pattern to this index is fine.

**Pseudocode:**

```python
def singleNonDuplicate(self, nums: List[int]) -> int:
	left, right = 0, len(nums)-1
	while left < right:
		mid = (left + right) // 2
		# if index is odd, make it even to apply my check
		if mid % 2:
			mid -= 1
		# if out of bounds, it would check nums[0]
		# -> no bounds check needed
		if nums[mid] != nums[mid+1]:
			right = mid
		else:
			# +2 because of the pairs
			left = mid + 2
	return nums[left]
```

**Complexity Analysis:**

- Time: O(log n) - Binary search time complexity.
- Space: O(1) - No extra memory.

**Learnings:**

- When the pairs are present in an array problem the odd/even indices become very useful and will most likely lead to a solution. For example in palindrome problems the same can be applied.
- If there's no apparent reoccurrence for the binary search (or any other array problem) take a look at the indices.

**Next Steps:**

- Look for indices in problems when pairs are present in any form (duplicates, given pairs, palindromes).