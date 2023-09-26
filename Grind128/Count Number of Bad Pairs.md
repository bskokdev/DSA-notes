**Problem Statement:**
given a **0-indexed** integer array `nums`. A pair of indices `(i, j)` is a **bad pair** if `i < j` and `j - i != nums[j] - nums[i]`.

Return _the total number of **bad pairs** in_ `nums`.

**Approach & pattern used:**
- I first thought I was supposed to use 2 pointers but then I would obviously miss some pairs.
- Brute force would be to iterate for each `i` through the entire array and find matching pairs.
- However I can be instead looking for the good pairs and then subtract it from the total pairs count:
	- `res = total_count - good_pairs`
- How do I find the good pairs?
	- Let's reverse the statement condition:
		- `i >= j or j - i == nums[j] - nums[i]`
		- Now let's simplify this:
			- `j - nums[j] = i - nums[i]`
	- This means if I've seen `i - nums[i]` before I have a valid pair. Therefore I can add `mp[i-num]` to the good pairs count and increment `mp[i-num]` by 1.

**Pseudocode:**

```python
def countBadPairs(self, nums: List[int]) -> int:
	n = len(nums)
	total = n * (n-1) // 2
	good = 0
	lookup = defaultdict(int)
	for i, num in enumerate(nums):
		cur_pair = i - num
		good += lookup[cur_pair]
		lookup[cur_pair] += 1
	return total - good
```

**Complexity Analysis:**

- Time: O(n) - Single iteration.
- Space: O(n) - Lookup map.

**Learnings:**

- Sequence has **`n * (n-1) // 2` pairs**.
- **I can get a lookup condition if I simplify the initial equation.**
- **I can reverse the problem definition and actually do the opposite** of what the problem is asking - instead of finding bad pairs, I found the good pairs which is simpler.

**Next Steps:**

- Try to apply the "reverse" definition method on other problems