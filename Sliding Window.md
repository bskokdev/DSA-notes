## General Overview
- We hold a state of a window in a **Data Structure (set, map) or a variable (sum)**
	- **set** - when we don't want repeated chars in the window etc
	- **map** - count occurrences
- The state is updated whenever the right pointer moves
- The left pointer is moved when the window doesn't meet conditions
	- Window contains duplicates; window size > k
	- We need to remove the value at the left pointer from our state and even remove memory from the Data Structure
- To calculate window size use this formula: 
```python
right-left+1
```

Example: 
```python
    def characterReplacement(self, s: str, k: int) -> int:
	    # freq & max_freq is the state of the window
        freq = defaultdict(int)
        left = res = max_freq = 0
        
        for right in range(len(s)):
	        # update the state
            freq[s[right]] += 1
            max_freq = max(max_freq, freq[s[right]])
            lowest_freq = (right-left+1) - max_freq
            # Doesn't meet conditions
            # lowest_freq is over k
            # We move left pointer and update the state
            if lowest_freq > k:
                freq[s[left]] -= 1
                left += 1
            if freq[s[left]] == 0:
                del freq[s[left]]
            res = max(right-left+1, res)
        return res
```
## Fixed Size Window
- It's usually fixed off of a given size (length of a subarray, given k)
- We can precompute the first window
	- Then we move our right and left pointer by 1 on each iteration
	- Don't forget to maintain the correct state

