**Problem Statement:**
Find the and return the index of the target number in a possibly rotated sorted array. The initial array before rotation is sorted.

**Input:** nums = [4,5,6,7,0,1,2], target = 0
**Output:** 4

**Approach & pattern used:**
- At most I have 2 subarrays which are both sorted.
- This means I need to apply binary search and select correct subarray to look for the target.
- The key is to figure out if the `array[left:mid+1]` is in sorted order or not.
	- `if nums[left] <= nums[mid]`
	- If this is true, then the right subarray including the middle element is in a valid sorted order.
	- Now I need to check if the target is present here or in the right subarray.
		- `if target < nums[left] or target > nums[mid]`:
			- target is in the right subarray
			- therefore: `left = mid + 1`
		- else the target in our current subarray:
			- `right = mid - 1`
- If `array[left:mid+1]` **is not** in a valid sorted order it means I found a split.
	- In other words `nums[left] > nums[mid]`
	- if the target is greater than the last element of the right subarray: `if target > nums[right]` or if it is possibly smaller than my mid element `if target < nums[mid]`
		- I know it's in the left subarray as it cannot fit to the right subarray
		- `right = mid - 1`
	- else we know it's in the right subarray
		- `left = mid + 1`
- If I don't find it, return -1

**Pseudocode:**

```python
def search(self, nums: List[int], target: int) -> int:
	left, right = 0, len(nums)-1
	while left <= right:
		mid = (left + right) // 2
		# We found target
		if nums[mid] == target:
			return mid
		# Valid sorted order
		if nums[left] <= nums[mid]:
			# Target cannot be in the left subarray
			if target < nums[left] or target > nums[mid]:
				left = mid + 1
			else:
				right = mid - 1
		# Split
		else:
			if target > nums[right] or target < nums[mid]:
				right = mid - 1
			else:
				left = mid + 1
	return -1
```

**Complexity Analysis:**

- Time: O(log n) - Binary search.
- Space: O(1) - No extra memory.

**Learnings:**

- I don't need an entire sorted array to apply binary search on it.
- All I need is some monotonic property
	- In this case 2 subarrays are guaranteed to be sorted

**Next Steps:**

- Try to notice monotonic properties of arrays if asked to optimize solution even further than O(n).