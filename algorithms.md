# Big O Notation
What is Big O notation?
Big O notation measures the complexity of algorithms.
It measures the way complexity grows relative to an algorithms input. It talks about the relationship between an algorithm's input size and its runtime.

f(n) could be linear = f(n) = n - the complexity scales with the size of the input = O(n)
f(n) could be constant = f(n) = 1 - the complexity stays the same regardless of input = O(1)

If you have a NESTED loop (one O(n) algorithm inside another), the complexity is *squared* if the second loop is also iterating over the same input = O(n^2)
If the inner loop's iterations do not scale with the input, the complexity would still be 0(n). (I think).

## Time complexity
## Space complexity
