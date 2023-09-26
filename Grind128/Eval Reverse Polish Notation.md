**Problem Statement:**
- Given an array of tokens which represent either numbers or operations evaluate reverse polish notation. No divisions by 0 are present.

**Approach & pattern used:**
- I can use stack for this.
- If I come across a token which is not a number but rather an math expression ("+", "-", "*", "/"):
	- I evaluate previous 2 values.
	- Then store the result back in the stack.
- My result is present at the top of the stack after performing all math operations.

**Pseudocode:**

```python
def evalRPN(self, tokens: List[str]) -> int:
	def evaluate(a, b, op):
		if op == "+":
			return a + b

		if op == "-":
			return a - b

		if op == "*":
			return a * b

		if op == "/":
			return a / b

	stack = []
	for token in tokens:
		# I come across math expression
		if (
		token == "+" or token == "-" or
		token == "*" or token == "/"):

			# I take 2 last values from the stack
			a = stack.pop()
			b = stack.pop()

			# Evaluate (careful with order) & store
			res = int(evaluate(b, a, token))
			stack.append(res)

		# Normal int value, so I just append
		else:
			stack.append(int(token))

	return stack[-1]
```

**Complexity Analysis:**

- Time: O(N) - Tokens array iteration.
- Space: O(N) - Stack of values.

**Learnings:**

- **When using stack to solve a problem I can pop as many values as I want not only the last one.**
- This **allows** me to perform **operations on previous n values**.
- Also I can store the result of such operation in the stack for later reuse.
**Next Steps:**

- 