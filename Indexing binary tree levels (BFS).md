- We do classic BFS level order traversal on a binary tree and also store current position for each node -> **(node, position)**
- To calculate children positions use following formulas:
```python
left_child_pos = 2 * cur_pos
right_child_pos = 2 * cur_pos + 1
```

**Example usage:**
```python
def widthOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        res = 0
        q = deque([(root, 0)])
        while q:
            _, first_pos = q[0]
            last_pos = -1
            for _ in range(len(q)):
                cur, pos = q.popleft()
                last_pos = pos
                if cur.left:
                    q.append((cur.left, 2*pos))
                if cur.right:
                    q.append((cur.right, 2*pos+1))
            res = max(last_pos-first_pos+1, res)
        return res
```
