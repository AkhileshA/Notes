# Chapter - 2

# Introduction

Here we are comparing the initial algorithms that were discussed previously, insertion sort and merge sort. 

# How is an algorithm identified as a correct one?

They take insertion sort as an example for this. In insertion sort with an array `A` and if the iteration variable is `i`.  At any point in the iteration the sub-array `A[1:i-1]`  is always sorted. This condition is called the `loop invariant`.

Loop invariants help us understand why an algorithm is correct. When using a loop invariant, you need to demonstrate three things:

**Initialisation:** It is true prior to the first iteration of the loop.

**Maintenance:** If it is true before an iteration of the loop, it remains true before the next iteration.

**Termination:** The loop terminates. When it does, the invariant, usually combined with the reason why the loop terminated, provides a useful property that helps demonstrate the algorithm's correctness.

# Analysis of algorithms

Many factors influence the execution time of an algorithm. 

- Size of input.
- How many operations required to solve for the input. (if the input is already mostly sorted)

# Important points

- Sometimes in the real world you might have to also consider the affects of the memory hierarchy in a computer like caches and virtual memory.
- While analysing the running time of an algorithm it can be important to measure it for both the worst case and the best for the same input size. For some algorithms, it might not even depend on the input like the recursive merge sort.
- It is important to keep in mind the probability of the type of inputs that can occur for an algorithm.