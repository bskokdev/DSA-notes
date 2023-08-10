## Overview
Very useful for calculating sum ranges in an array. We can access the sum up to K elements by looking up the prefix sum of the Kth number.

For example, suppose this int array: `nums = [1,2,3,4,5]`

Prefix sum allows us to calculate the sum up to the last element by calling `prefix_sum[5]` = `15`.

The prefix sum of the example int array would look like this:
`p_sum = [0,1,3,6,10,15]`.

**Note:** We use 1-indexed version of the prefix sum array, therefore it stores `n+1` elements where `n` is the size of the initial array - `[1,2,3,4,5]` is our case.

## Useful formulas
Since we use 1-indexed version of the prefix sum, we need to calculate with some index offset.

#### Build a 1-indexed prefix sum
To build the prefix sum array, we would then use this formula on each iteration of i:
```python
nums = [1,2,3,4,5]
n = len(nums)

prefix_sum = [0] * (n+1)
for i in range(1, n+1):
	prefix_sum[i] = nums[i-1] + prefix_sum[i-1]
```
**Note:** Iteration starts at index 1, so we are within the bounds and goes all the way to the `n+1` since we are in the 1-indexed array. This takes O(n) time to build.

#### Sum queries
Probably the most common usage of the prefix sum is for answering sum queries on a given range. Suppose again we have an int array `nums = [1,2,3,4,5]` (0 indexed) and we want to calculate the sum of numbers at indexes 2-4 - let's call them `R` and `L` pointers, where `R = 2` and `L = 4`.

We can just simply build the prefix sum using the previous formula and then subtract `R+1` from the `L` pointer values. We use `R+1` because remember, we use 1-indexed prefix sum, therefore, the offset is necessary.

Therefore, the formula for answering the queries on a given range is this:
```python
range_sum = prefix_sum[R+1] - prefix_sum[L]
```

**Note:** You can certainly use 0-indexed prefix sum, however, you need to be careful with the indexes.
I find using the 1-indexed prefix sum a bit more intuitive though as we can just say to get the prefix sum of first K elements.
**Don't forget sums are not the only use case - products, frequency counts can also be solved by using the prefix sum.**