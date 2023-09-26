```java
// This can be number of possible subsets
x << k == x * 2^k

// Check if the jth bit of integer x is set to 1
// This is how we can detect if there's a subset
// 000010 -> subset from the 2nd bit (from left) to the right
x & (1 << j) != 0 
```

