## Overview
- We use it when we need to use **dictionary** for non-primitive data types such as **Tree nodes, Graph nodes** etc.
- We convert this data type to a **unique string (hash)** which will then be used as a key in a dictionary and allows us fast lookup times
```python
duplicates = []
seen = defaultdict(int)
def ser(node: TreeNode):
	if not node:
		return "#"
		
	h_key = f'{node.val}, {ser(node.left){ser(node.right)}'
	seen[h_key] += 1
	if seen[h_key] == 2:
		duplicates.append(node) 
	return h_key
```