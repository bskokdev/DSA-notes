## In-order
##### We go deep to the left first, then root, then right
- **When I need a sorted order**
- **BST problems** (validation, etc.)
- Tree flattening into an array or linked list

## Pre-order
##### First root then left & right.
- The most common type for tree problems
- Tree copies
- Serialization
- Paths to leaf nodes

## Post-order
##### Left & right first, then root.
- Postfixes
- DP
## Level-order
- Shortest paths in trees (minimum amount of levels traversed)
- Operations based on levels

## Additional tips
- If I see a tree don't think of generic graph DFS, but rather which traversal do I use here.
	- Decide based on the constraints.
- In-order is more efficient as it can exit earlier.