## What do I mean by this
You could be given 2 different input arrays of edges where each array could categorize the edge. For example, let's say you were given 2 arrays of red and blue edges 
`redEdges: List[List[int]], blueEdges: List[List[int]]`

## How to approach this kind of problem
You want the to keep track of overlapping nodes, to achieve this use this pattern and change `red, blue` categories to match current categories.
```python
graph = defaultdict(lambda: defaultdict(set))
red, blue = True, False

for src, dst in redEdges: graph[src][red].add(dst)
for src, dst in blueEdges: graph[src][blue].add(dst)
```
Here we create a dictionary of dictionaries, each of them keeps a adjacency list graph representation for each category.
We can therefore fast access and know in which category the given node is.