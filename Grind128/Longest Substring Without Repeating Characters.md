**Problem Statement:**
- Find the longest substring in the given string s without repeating characters

**Approach & pattern used:**
- Substring/subarray without subproblems means **sliding window** pattern.
- To handle the duplicates we use **set**
	- I can roll any data structure over the window as necessary - sets, hash maps, sum, etc.
- In this problem I just iterate over the `len(s)` using a for loop. This will be my right pointer of the window.
	- if `s[right] is not in seen`:
		- update `res = max(res, window size)`.
	- else - `s[right] is in seen set already`:
		- I remove `s[left]` from the `seen` set and move left pointer by 1.
	- At the end of iteration I insert `s[right]` to the set.

**Pseudocode:**

```python
def lengthOfLongestSubstring(self, s: str) -> int:
	seen = set()
	left = res = 0
	for right in range(len(s)):
		if s[right] not in seen:
			res = max(res, right-left+1)
		else:
			while s[right] in seen:
				seen.remove(s[left])
				left += 1
		seen.add(s[right])
	return res
```

**Complexity Analysis:**

- Time: O(n) - Single for loop.
- Space: O(n) - Extra seen set.

**Learnings:**

- I can run a data structures along the sliding window
- I don't have to update result only on the "wrong" condition we we move the left pointer but also on the expected condition - I calculate res in the above problem if `s[right]` meets the condition. This will come in handy if after moving `left += 1` will not give the correct result.
- I can run a `while` loop to eliminate all incorrect values from the data structure we run alongside the window.

**Next Steps:**

- Think of the correct (if any) data structure to run along the window.
- Choose wisely on which condition we should update the result variable.