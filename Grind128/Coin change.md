**Problem Statement:**
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the fewest number of coins that you need to make up that amount_.

**Approach & pattern used:**
- I can select any of the coins so it basically forms a subsequence in the array, therefore DP is used.
- My subproblem is selecting the coins
	- The search space per DFS call are all the coins.
	- What I care about is the minimal number of coins used at current amount, so I can explore all the possible paths and pick the minimal one. This would by my result. 

**Pseudocode:**

```python
def coinChange(self, coins: List[int], amount: int) -> int:
	n = len(n)
	memo = {}
	def dfs(cur_amount):
		if cur_amount in memo:
			return memo[cur_amount]
		if cur_amount < 0:
			return -1
		if cur_amount == 0:
			return 0

		# Keep min of all possible paths
		min_coins_used = float('inf')
		# Explore the search space
		for coin in coins:
			cur_coins_used = dfs(cur_amount - coin)
			if (
			cur_coins_used >= 0 and
			cur_coins_used < min_coins_used):
				min_coins_used = cur_coins_used
				
		if min_coins_used == float('inf'):
			memo[cur_amount] = -1
			return memo[cur_amount]
			
		memo[cur_amount] = min_coins_used
		return memo[cur_amount]
```

**Complexity Analysis:**

- Time: O(n ^ m) - *N* decisions of size of the entire array.
- Space: O(n + m) - Recursion stack + memo.

**Learnings:**

- **DFS == going a certain path or direction.**
- **Dynamic Programming is basically educated recursive guess with cache.**
- In the decision tree I can get max/min from the paths my keeping a variable above the search space: `min_coins_used`.
	- This is useful in problems when I need to explore a certain option space and get the min/max result.


**Next Steps:**

- This of DFS calls as: Now I go this path.
	- Apply it for:
		- Binary Trees
		- Graphs
		- Decision Trees