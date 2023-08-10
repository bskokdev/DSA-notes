## Trie implementation
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        cur = self.root
        for c in word:
            if c not in cur.children:
                cur.children[c] = TrieNode()
            cur = cur.children[c]
        cur.is_word = True

    def search(self, word: str) -> bool:
        node = self.find_node(word)
        return node is not None and node.is_word

    def startsWith(self, prefix: str) -> bool:
    """
    Returns if there's a prefix in the Trie
    """
        return self.find_node(prefix)

    def find_node(self, string) -> Optional[TreeNode]:
    """
    Finds the last node in the Trie for a given string
    """
        cur = self.root
        for char in string:
            if char not in cur.children:
                return None
            cur = cur.children[char]
        return cur
```

Above's the generic Trie DS implementation supporting inserting, finding word and finding prefix operations. However, the most important part of the Trie is the `TrieNode` class. Why?
With this class alone we can simulate the entire Trie and therefore implementing the entire `Trie` class is not necessary, although more structured.

## TrieNode
- Has to hold the children in a `dict` or children TrieNode array (max 26 children `TrieNodes` in both cases)
- **Can hold additional state**
	- This could be just a word, list of words etc.
```python
class TrieNode:
    def __init__(self):
        self.children = defaultdict(TrieNode)
        self.suggestions = []

    def add_suggestion(self, product):
        if len(self.suggestions) < 3:
            self.suggestions.append(product)
```

## Basic pure TrieNode usage
In our solution we can just create this `root TrieNode` which would act as our `Trie`. Then in the rest of our function we can add words to that `root node` as we would in the Trie data structure implemented at the top.
```python
# Add all words to the Trie from the input
for word in words:
	# Trie iteration (same as at top)
	cur = trie
	for char in word:
		if char not in cur.children:
			cur.children[char] = TrieNode()
		cur = cur.children[char]
```

Also in this process instead of creating new `TrieNodes` we could be modifying the state of a `TrieNode` for each char.
Consider this `TrieNode` implementation:
```python
class TrieNode:
    def __init__(self):
        self.children = defaultdict(TrieNode)
        self.suggestions = []

    def add_suggestion(self, product):
        if len(self.suggestions) < 3:
            self.suggestions.append(product)
```
We could modify the state in this way:
```python
# Add products to the Trie
for product in products:
	# Trie iteration
	node = trie
	for char in product:
		node = node.children[char]
		node.add_suggestion(product)
```
