## General usage
- I use try whenever I need to check for a prefix or a word.
- **String lookups in general**
	- This could be implementing:
		- **PREFIX SEARCH**
		- **Wildcard matching**
		- **Autocomplete or suggestions**
		- Multiple queries into a single result
		- Breaking words
		- Multiple types of lookups on a dictionary
- **When doing custom logic (i.e. wildcard matching) with the Trie use recursion**
	- *Because it's a Tree and **Tree = recursive** DS*

### Implementation

```python
class TrieNode:
	def __init__(self):
		self.children = {}
		self.is_word = False

class Trie:
	def __init__(self):
		self.root = TrieNode()

	def insert(self, word: str) -> None:
		node = self.root
		for char in word:
			if char not in node.children:
				node.children[char] = TrieNode
			node = node.children[char]
		node.is_word = True

	def has_word(self, word: str) -> None:
		node = self.find_node(word)
		return node and node.is_word
		
	def has_prefix(self, word: str) -> None:
		return self.find_node(word)

	
	def find_node(self, word: str) -> None:
	"""
	# Helper method to find a node for a string
	"""
		node = self.root
		for char in char:
			if char not in node.children:
				return None
			node = node.children[char]
		return node
```
